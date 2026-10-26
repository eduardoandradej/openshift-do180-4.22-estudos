# Revisão — Capítulo 3

Questões **autorais**. Elas não reproduzem o quiz oficial nem perguntas de exame.

## Parte 1 — Conceitos

1. Por que o curso recomenda `oc run` só para depuração e tarefas temporárias?
2. Explique o formato `base/tamanho` da anotação `openshift.io/sa.scc.uid-range`.
3. Por que o GID primário 0 não torna o processo privilegiado?
4. Qual a diferença entre PSA e SCC?
5. O que diferencia o CRI-O do Podman?
6. Diferencie tag fixa, tag flutuante e digest.
7. Para que serve a `ClusterImagePolicy` e o que mudou no 4.22?
8. Por que alterar um container em execução não é uma correção definitiva?

## Parte 2 — Comandos (escreva o comando)

9. Criar um Pod `teste` com a imagem `registry.access.redhat.com/ubi10/ubi` que imprime `uname -r`, não reinicia e é apagado ao final.
10. Ver os logs da instância anterior do container `app` no Pod `loja-1`.
11. Listar as tags de `registry.access.redhat.com/ubi10/python-312` sem baixar a imagem.
12. Mostrar usuário, entrypoint e comando da imagem do item 11.
13. Copiar `./app.conf` para `/opt/app-root/etc/` no Pod `api-0`.
14. Abrir um túnel da porta local 15432 até a porta 5432 do Pod `pg-0`.
15. Trocar a imagem do primeiro container do Pod `web` para `registry.access.redhat.com/ubi10/httpd-24:latest` sem abrir editor.
16. No nó, obter o PID do container `postgresql` e listar seus namespaces.

## Parte 3 — Diagnóstico

17. Pod em `ErrImagePull` com a mensagem `manifest unknown`. Causa e correção?
18. Pod de uma imagem Nginx do Docker Hub entra em `CrashLoopBackOff`; os logs mostram `Permission denied` em `/var/cache/nginx`. Explique e proponha soluções.
19. `oc cp` falha com erro sobre `tar`. O que fazer?
20. A aplicação em `Running` não responde pela Route, e você não sabe se o problema é a aplicação ou a rede. Como isolar a causa?

---

<details>
<summary>Respostas comentadas</summary>

1. Pods avulsos não são recriados se falharem ou se o nó cair, e não têm rollout. Para produção usam-se manifestos declarativos com Deployment e outros recursos de workload.
2. `1000710000/10000`: começa em 1000710000 e reserva 10.000 IDs. Cada projeto recebe um bloco diferente.
3. O UID é alto e não root, e são as permissões do UID que determinam o privilégio no kernel. O grupo 0 só permite usar arquivos com permissão para o grupo root.
4. PSA (Kubernetes) aplica perfis `privileged`/`baseline`/`restricted` por namespace e avisa sobre *security contexts*; SCC (OpenShift) define padrões seguros e concede as permissões compatíveis com o perfil.
5. O CRI-O é um runtime feito para o Kubernetes (interface CRI), integrado a plugins de rede e storage e usado pelo kubelet; o Podman é uma ferramenta de uso geral para pessoas.
6. Tag fixa aponta para um build específico; flutuante é um apelido que muda (ex.: `10.0`, `latest`); digest é o hash imutável do conteúdo.
7. Define políticas de verificação de assinatura (Sigstore) para imagens do cluster; o MCO aplica em `/etc/containers/policy.json`. No 4.22 a verificação cobre cada camada da imagem.
8. A mudança fica no sistema de arquivos efêmero, não é registrada em controle de versão e some quando o Pod é recriado.
9. `oc run teste -it --rm --restart Never --image registry.access.redhat.com/ubi10/ubi --command -- uname -r`
10. `oc logs loja-1 -c app --previous`
11. `skopeo list-tags docker://registry.access.redhat.com/ubi10/python-312`
12. `skopeo inspect --config docker://registry.access.redhat.com/ubi10/python-312:latest | jq '.config | {User, Entrypoint, Cmd}'` (ou `oc image info ...`).
13. `oc cp ./app.conf api-0:/opt/app-root/etc/`
14. `oc port-forward pod/pg-0 15432:5432`
15. `oc patch pod web --type=json -p '[{"op":"replace","path":"/spec/containers/0/image","value":"registry.access.redhat.com/ubi10/httpd-24:latest"}]'`
16. `crictl ps --name postgresql` → `crictl inspect -o json <id> | jq .info.pid` → `lsns -p <PID>` (dentro de `oc debug node/<nó>` + `chroot /host`).
17. A tag (ou o repositório) não existe no registry. Liste as tags com `skopeo list-tags` e corrija a referência da imagem.
18. A imagem espera rodar como root; no OpenShift, um usuário comum roda com UID aleatório e GID 0, sem permissão nesse diretório. Soluções: usar uma imagem preparada para não root (ex.: as da Red Hat) ou ajustar a imagem para dar ao grupo 0 permissão de escrita. Rodar como root exigiria permissões de administrador e não é recomendado.
19. A imagem não tem `tar`. Use `oc rsync` (se houver `rsync`), envie o conteúdo por `oc exec -i ... -- sh -c 'cat > arquivo'` (se houver shell), ou leve o arquivo para a imagem ou para um volume/ConfigMap.
20. `oc port-forward` até a porta do Pod e `curl` local. Se responder, o problema está na cadeia Service/Route (Capítulo 4); se não, na aplicação (`oc logs`, `oc exec`).

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 18–20 | Siga para o Capítulo 4 |
| 14–17 | Refaça a Parte C das lições onde errou |
| < 14 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
