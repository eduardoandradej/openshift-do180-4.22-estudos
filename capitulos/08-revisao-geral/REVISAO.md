# Revisão integrada — Capítulos 1 a 7

Dois **simulados autorais**, por especificação e com tempo, para treinar antes dos
labs 8.2 e 8.3. O cenário é **original** ("Biblioteca Digital") e não reproduz os
enunciados oficiais.

> **Onde praticar:** em um cluster próprio (Red Hat OpenShift Local ou Developer
> Sandbox), nunca durante uma atividade oficial. Ajuste a StorageClass ao seu
> cluster (`oc get storageclass`). Algumas imagens de `registry.redhat.io` exigem
> credenciais de pull configuradas no cluster. Todos os valores de senha são fictícios.

---

## Simulado A — Implantar a Biblioteca Digital (tempo-alvo: 40 min)

### Especificação

1. Projeto **`biblioteca`**.
2. Secret **`db-cred`** com as chaves `user=leitor`, `password=Troque-me-123`, `database=acervo`.
3. ImageStream **`postgres`** com a tag **`16`** apontando para
   `registry.redhat.io/rhel9/postgresql-16:latest`, utilizável **pelo nome curto** no projeto.
4. Deployment **`acervo-db`** usando a imagem pelo nome curto `postgres:16`:
   - variáveis `POSTGRESQL_USER`, `POSTGRESQL_PASSWORD`, `POSTGRESQL_DATABASE` vindas do Secret (prefixo `POSTGRESQL_`);
   - PVC **`acervo-data`** de **1Gi**, **RWO**, StorageClass do seu cluster, montado em `/var/lib/pgsql/data` com o volume chamado **`dados`**;
   - **image trigger** no container para a tag `postgres:16`.
5. Service **`acervo-db`** na porta **5432**.
6. ConfigMap **`vitrine-html`** com um arquivo `index.html` contendo o texto `Biblioteca Digital`.
7. Deployment **`vitrine`** com `registry.access.redhat.com/ubi10/httpd-24`:
   - variáveis `APP_USER`, `APP_PASSWORD`, `APP_DATABASE` do mesmo Secret (prefixo `APP_`) e `APP_DBHOST=acervo-db`;
   - ConfigMap montado em `/var/www/html`.
8. Service **`vitrine`** na porta **80** encaminhando para **8080**.
9. Route **`vitrine`** com hostname gerado automaticamente.
10. Teste: `curl` na Route retorna `Biblioteca Digital`.

### Checklist de verificação

- [ ] `oc get is postgres` mostra a tag `16` e `oc set image-lookup` mostra `true`.
- [ ] `oc set env deployment/acervo-db --list` mostra as três variáveis vindas de `secret/db-cred`.
- [ ] `oc get pvc acervo-data` está `Bound` (ou `Pending` até o Pod, se a classe usar `WaitForFirstConsumer`).
- [ ] `oc set triggers deployment/acervo-db` mostra o trigger `image` com `AUTO true`.
- [ ] `oc get endpointslices -l kubernetes.io/service-name=acervo-db` lista o IP do Pod.
- [ ] `oc get svc vitrine` mostra `80/TCP` e `targetPort` 8080.
- [ ] `curl` na Route responde o conteúdo esperado.

<details>
<summary>Solução de referência (abra só depois de tentar)</summary>

```bash
oc new-project biblioteca
oc create secret generic db-cred \
  --from-literal user=leitor --from-literal password='Troque-me-123' --from-literal database=acervo

oc import-image postgres:16 --from registry.redhat.io/rhel9/postgresql-16:latest --confirm
oc set image-lookup postgres

oc create deployment acervo-db --image postgres:16
oc set env deployment/acervo-db --from secret/db-cred --prefix POSTGRESQL_
oc set volumes deployment/acervo-db --add --name dados --type pvc \
  --claim-name acervo-data --claim-size 1Gi --claim-mode rwo \
  --claim-class <SUA_STORAGECLASS> --mount-path /var/lib/pgsql/data
oc get deployment acervo-db -o jsonpath='{.spec.template.spec.containers[0].name}{"\n"}'
oc set triggers deployment/acervo-db --from-image postgres:16 --containers <NOME_DO_CONTAINER>
oc expose deployment/acervo-db --port 5432

echo 'Biblioteca Digital' > index.html
oc create configmap vitrine-html --from-file=index.html

oc create deployment vitrine --image registry.access.redhat.com/ubi10/httpd-24
oc set env deployment/vitrine --from secret/db-cred --prefix APP_
oc set env deployment/vitrine APP_DBHOST=acervo-db
oc set volume deployment/vitrine --add --type configmap \
  --configmap-name vitrine-html --mount-path /var/www/html
oc expose deployment/vitrine --port 80 --target-port 8080
oc expose service vitrine
curl -s http://$(oc get route vitrine -o jsonpath='{.spec.host}')/
```

Observações:

- O nome do container criado por `oc create deployment` costuma derivar do nome da imagem (aqui, `postgres`). Por isso a solução consulta o nome antes do trigger.
- Com `--prefix POSTGRESQL_`, as chaves `user`, `password` e `database` viram `POSTGRESQL_USER`, `POSTGRESQL_PASSWORD` e `POSTGRESQL_DATABASE`.
- Se o Pod do banco falhar, veja `oc logs deploy/acervo-db`: credenciais e permissões do diretório de dados são as causas usuais.

</details>

---

## Simulado B — Diagnosticar, endurecer e escalar (tempo-alvo: 25 min)

### Preparação do cenário (rode antes de iniciar o cronômetro)

Partindo do Simulado A concluído, introduza falhas propositais:

```bash
oc project biblioteca
oc set image deployment/vitrine httpd-24=registry.access.redhat.com/ubi10/httpd-24:nao-existe
oc set resources deployment/acervo-db --requests memory=512Gi
oc create deployment ruido --image registry.access.redhat.com/ubi10/ubi \
  -- /bin/bash -c 'while true; do :; done'
```

> Se o nome do container da `vitrine` não for `httpd-24`, ajuste o primeiro comando
> (`oc get deployment vitrine -o wide`).

### Especificação

1. Identifique o workload que consome CPU sem utilidade e remova-o.
2. Faça o `acervo-db` voltar a rodar, com **requests** de `250m` de CPU e `256Mi` de memória e **limits** de `500m` e `512Mi`.
3. Adicione ao `acervo-db` uma **readiness** e uma **liveness** por comando, usando `pg_isready -h 127.0.0.1`.
4. Faça a `vitrine` voltar a rodar com uma imagem válida, **fixada por tag estática ou digest** (não `latest`).
5. Adicione à `vitrine` uma **readiness** HTTP em `/` na porta 8080 e uma **liveness** TCP na porta 8080.
6. Defina na `vitrine` requests `100m`/`128Mi` e limits `300m`/`256Mi`.
7. Aplique os itens 4 a 6 da `vitrine` em **um único rollout**.
8. Escale a `vitrine` para **3 réplicas** e crie um **HPA** entre 3 e 6 réplicas com alvo de 70% de CPU.
9. Registre no histórico do Deployment `vitrine` o motivo da última mudança.
10. Confirme: Route respondendo, 3 endpoints na `vitrine`, HPA com métrica (não `<unknown>`).

### Checklist de verificação

- [ ] `oc adm top pods` (ou console › *Overview*) identificou o consumidor; o Deployment foi removido.
- [ ] `oc get pods` sem `Pending`, `ImagePullBackOff` ou `CrashLoopBackOff`.
- [ ] `oc describe deployment acervo-db` mostra `Readiness`/`Liveness` com `exec`.
- [ ] `oc get deployment vitrine -o jsonpath='{.spec.template.spec.containers[0].image}'` não termina em `latest`.
- [ ] `oc rollout history deployment/vitrine` mostra uma única revisão nova e o `CHANGE-CAUSE`.
- [ ] `oc get hpa vitrine` com `TARGETS` numérico.

<details>
<summary>Solução de referência (abra só depois de tentar)</summary>

```bash
# 1. Consumidor de CPU
oc adm top pods --sort-by=cpu
oc delete deployment ruido

# 2. Banco: request impossível → FailedScheduling
oc describe pod -l app=acervo-db | grep -A3 Events
oc set resources deployment/acervo-db --requests cpu=250m,memory=256Mi --limits cpu=500m,memory=512Mi

# 3. Probes do banco
oc set probe deployment/acervo-db --readiness -- pg_isready -h 127.0.0.1
oc set probe deployment/acervo-db --liveness  -- pg_isready -h 127.0.0.1

# 4–7. Vitrine em um único rollout
skopeo list-tags docker://registry.access.redhat.com/ubi10/httpd-24      # escolher uma tag estática
oc rollout pause deployment/vitrine
oc set image deployment/vitrine httpd-24=registry.access.redhat.com/ubi10/httpd-24:<TAG_ESTATICA>
oc set probe deployment/vitrine --readiness --get-url http://:8080/
oc set probe deployment/vitrine --liveness --open-tcp 8080
oc set resources deployment/vitrine --requests cpu=100m,memory=128Mi --limits cpu=300m,memory=256Mi
oc rollout resume deployment/vitrine
oc rollout status deployment/vitrine

# 8. Escala e HPA
oc scale deployment/vitrine --replicas 3
oc autoscale deployment/vitrine --min 3 --max 6 --cpu 70%

# 9. Motivo
oc annotate deployment/vitrine kubernetes.io/change-cause="Tag estática, probes e recursos" --overwrite

# 10. Verificação
oc get endpointslices -l kubernetes.io/service-name=vitrine
oc get hpa vitrine
curl -s http://$(oc get route vitrine -o jsonpath='{.spec.host}')/
```

Observações:

- O banco ficava `Pending` (`Insufficient memory`): é uma falha de **agendamento**, não da aplicação.
- A `vitrine` ficava em `ImagePullBackOff`: tag inexistente. Antes de corrigir, `oc rollout undo` também resolveria, mas a especificação pede tag estática.
- Com o HPA criado, o número de réplicas passa a ser controlado por ele; o mínimo 3 mantém a alta disponibilidade.

</details>

---

## Questões integradas (sem cronômetro)

1. Uma aplicação implantada com `:latest` mostrou versões diferentes entre réplicas depois de uma escala. Explique a causa (Cap. 7) e duas soluções.
2. A Route responde 503, os Pods estão `Running` e `READY 0/1`. Que capítulos e comandos você usa para isolar a causa?
3. Por que um banco com três réplicas deve ser um StatefulSet e não um Deployment com um PVC?
4. Um Pod é recriado e perde um arquivo de configuração que você copiou com `oc cp`. Qual era a forma correta de entregar esse arquivo?
5. Como provar, só com a CLI, que o Pod em execução usa exatamente a imagem aprovada pela equipe de segurança?
6. Uma imagem de comunidade funciona no Podman, mas falha no OpenShift com `Permission denied`. Explique (Cap. 3) e proponha soluções.
7. Que combinação de recursos protege o nó de uma aplicação com vazamento de memória e, ao mesmo tempo, evita erros para clientes durante o reinício?

<details>
<summary>Respostas comentadas</summary>

1. Tag flutuante + `IfNotPresent`: nós diferentes tinham imagens diferentes para `latest`. Soluções: digest ou tag estática; ImageStream (com trigger para atualizações controladas).
2. Caps. 4 e 6: `oc get endpointslices` (vazio, porque os Pods não estão prontos) → `oc describe pod` (`Readiness probe failed`) → corrigir o caminho ou a porta da probe ou a dependência da aplicação.
3. Cada réplica precisa de dados próprios e identidade estável; um PVC compartilhado corromperia os dados e, se for RWO, nem montaria em outros nós (Cap. 5).
4. Um ConfigMap (ou Secret) montado como volume (Cap. 5); `oc cp` só altera o sistema de arquivos efêmero (Cap. 3).
5. `oc get pod <p> -o jsonpath='{.status.containerStatuses[*].imageID}'` e comparar com o digest aprovado (`oc image info`/`skopeo inspect`) (Cap. 7).
6. O OpenShift ignora o `USER` da imagem para usuários comuns e roda com UID aleatório e GID 0; a imagem esperava root. Usar uma imagem preparada para não root ou dar permissões ao grupo 0 na imagem (Cap. 3).
7. **Memory limit** (contém o vazamento com `OOMKilled` e reinício), **readiness** (tira do tráfego quem está reiniciando) e **várias réplicas** (as outras atendem) (Cap. 6).

</details>

## Autoavaliação final

| Resultado | Ação |
|-----------|------|
| Simulados dentro do tempo e questões corretas | Faça os labs 8.2 e 8.3; depois, DO280 |
| Simulados acima do tempo | Revise os `RESUMO.md` dos capítulos envolvidos e repita o simulado |
| Erros conceituais | Volte às lições indicadas e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
