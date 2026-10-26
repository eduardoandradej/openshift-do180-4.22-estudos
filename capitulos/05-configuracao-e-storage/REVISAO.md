# Revisão — Capítulo 5

Questões **autorais**. Elas não reproduzem atividades oficiais nem perguntas de exame.

## Parte 1 — Conceitos

1. Por que externalizar a configuração torna a imagem portável entre ambientes?
2. Explique a frase: "Secrets são codificados, não criptografados".
3. Compare variáveis de ambiente e volumes como forma de consumir ConfigMaps quanto à atualização.
4. Diferencie provisionamento estático e dinâmico.
5. Qual a diferença entre RWO e RWOP?
6. O que é a Storage Object in Use Protection?
7. Quando usar `Retain` em vez de `Delete`?
8. Qual a função do headless Service em um StatefulSet?

## Parte 2 — Comandos (escreva o comando)

9. Criar o Secret `api-cred` com `token=abc123` e `url=https://api.exemplo.com`.
10. Criar o ConfigMap `nginx-conf` a partir do arquivo `./default.conf`.
11. Montar `nginx-conf` em `/etc/nginx/conf.d` no Deployment `web`.
12. Injetar todas as chaves do Secret `db` como variáveis com prefixo `DB_` no Deployment `app`.
13. Baixar o conteúdo do Secret `db` para `/tmp/db`, sobrescrevendo se existir.
14. Adicionar ao Deployment `db` um PVC novo `db-data` de 5Gi, RWO, classe `lvms-vg1`, montado em `/var/lib/pgsql/data`.
15. Aumentar o PVC `db-data` para 10Gi.
16. Listar as StorageClasses e identificar a padrão.
17. Escalar o StatefulSet `cache` para 5 réplicas.

## Parte 3 — Diagnóstico

18. Um Pod fica em `CreateContainerConfigError`. Qual a causa provável neste capítulo?
19. Três réplicas de um Deployment usam um PVC RWO; uma roda, duas ficam em `ContainerCreating`. Explique e proponha soluções.
20. Após apagar um StatefulSet e recriá-lo, os dados antigos reapareceram. Por quê?

---

<details>
<summary>Respostas comentadas</summary>

1. A mesma imagem é usada em qualquer ambiente; o que muda são os ConfigMaps, Secrets e volumes de cada um, sem reconstruir a imagem.
2. Os valores ficam em base64, que qualquer leitor reverte. A criptografia em repouso exige habilitar a do etcd; o acesso deve ser restrito por RBAC.
3. Variáveis só são lidas no início do container (é preciso reiniciar); arquivos em volume são atualizados eventualmente pelo kubelet (exceto com `subPath`), e a aplicação precisa relê-los.
4. Estático: o administrador cria PVs antes, e os PVCs se ligam a eles. Dinâmico: o PVC referencia uma StorageClass, e o provisionador cria o PV sob demanda.
5. RWO limita a um **nó** (vários Pods desse nó podem montar); RWOP limita a um único **Pod**.
6. Proteção ativa por padrão que adia a remoção de um PVC usado por Pods (e de um PV ligado) até que deixem de estar em uso, evitando perda de dados.
7. Quando os dados não podem ser perdidos por um PVC apagado por engano; aceita-se o custo de limpeza manual.
8. Dá a cada Pod um nome DNS estável (`<pod>.<svc>`), permitindo descoberta entre pares e acesso a uma réplica específica.
9. `oc create secret generic api-cred --from-literal token=abc123 --from-literal url=https://api.exemplo.com`
10. `oc create configmap nginx-conf --from-file=./default.conf`
11. `oc set volume deployment/web --add --type configmap --configmap-name nginx-conf --mount-path /etc/nginx/conf.d`
12. `oc set env deployment/app --from secret/db --prefix DB_`
13. `oc extract secret/db --to /tmp/db --confirm`
14. `oc set volumes deployment/db --add --name db-data --type pvc --claim-name db-data --claim-size 5Gi --claim-mode rwo --claim-class lvms-vg1 --mount-path /var/lib/pgsql/data`
15. `oc patch pvc/db-data --type merge -p '{"spec":{"resources":{"requests":{"storage":"10Gi"}}}}'` (exige `allowVolumeExpansion: true`).
16. `oc get storageclass` (a padrão aparece com `(default)`).
17. `oc scale statefulset/cache --replicas 5`
18. O Pod referencia um ConfigMap ou Secret (ou uma chave) que não existe, sem `optional: true`. Veja `oc describe pod`.
19. RWO permite montar em **um nó**; as réplicas em outros nós não montam. Soluções: classe com RWX (ex.: NFS) se o compartilhamento for seguro para a aplicação; StatefulSet com um volume por réplica; ou manter uma réplica.
20. Apagar o StatefulSet não apaga os PVCs. Ao recriá-lo com o mesmo nome e template, cada Pod volta a montar `data-<sts>-<n>`.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 18–20 | Siga para o Capítulo 6 |
| 14–17 | Refaça a Parte C das lições onde errou |
| < 14 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
