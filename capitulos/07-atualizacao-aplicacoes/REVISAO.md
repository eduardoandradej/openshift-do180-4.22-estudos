# Revisão — Capítulo 7

Questões **autorais**. Elas não reproduzem atividades oficiais nem perguntas de exame.

## Parte 1 — Conceitos

1. Descreva dois cenários em que uma tag flutuante faz a aplicação mudar de versão sem que ninguém perceba.
2. Por que a diferença entre tag fixa e flutuante é só convenção, e o que dá garantia real?
3. Compare `IfNotPresent`, `Always` e `Never`, e diga qual é o padrão para `:latest`.
4. Quando escolher RollingUpdate e quando escolher Recreate?
5. Por que o Deployment guarda ReplicaSets antigos?
6. O que uma ImageStreamTag guarda que uma tag de registry não guarda?
7. Quais os três requisitos para um Deployment usar uma ImageStream pelo nome curto?
8. Como um alias de ImageStreamTag permite promover e reverter versões?

## Parte 2 — Comandos (escreva o comando)

9. Obter o digest da imagem `registry.access.redhat.com/ubi10/httpd-24:latest` para `linux/amd64`.
10. Trocar a imagem do container `web` do Deployment `site` para `registry.access.redhat.com/ubi10/httpd-24:10.0`.
11. Aplicar uma nova imagem e uma nova variável `MODO=prod` no Deployment `site` com um único rollout.
12. Ver o histórico de revisões do Deployment `site` e voltar à revisão 3.
13. Criar a ImageStreamTag `site:1.0` a partir de `quay.io/exemplo/site:1.0`, criando a ImageStream se necessário.
14. Fazer `site:1.0` verificar a origem periodicamente.
15. Habilitar o lookup local da ImageStream `site` e criar o Deployment `vitrine` com `site:1.0`.
16. Configurar o container `site` do Deployment `vitrine` para seguir `site:prod`.
17. Fazer `site:prod` seguir `site:1.1`.

## Parte 3 — Diagnóstico

18. Réplicas de um mesmo Deployment mostram `imageID` diferentes. Causa provável e prevenção?
19. Após `oc set image` com tag inexistente, o rollout não termina. O que acontece com os Pods antigos e o que fazer?
20. A ImageStreamTag foi atualizada, mas o Deployment continua com a imagem antiga. Cite duas causas.

---

<details>
<summary>Respostas comentadas</summary>

1. (a) Um Pod reagendado em outro nó baixa o `latest` novo; (b) ao escalar, Pods novos recebem a versão nova e os antigos ficam na anterior. Rollbacks também podem trazer uma imagem diferente da original.
2. Nada impede o publicador de reenviar outra imagem para uma tag "fixa". Garantia real: o **digest** (`@sha256:`) ou uma **ImageStreamTag**, que congela o digest.
3. `IfNotPresent`: usa a imagem local se existir. `Always`: consulta o registry e baixa se o digest mudou. `Never`: nunca baixa. Para `:latest` (ou sem tag) o padrão é `Always`.
4. RollingUpdate: versões compatíveis e sem indisponibilidade. Recreate: versões que não podem coexistir ou migrações de dados, aceitando indisponibilidade.
5. Para permitir **rollback** rápido (`oc rollout undo`), até o limite de `revisionHistoryLimit`.
6. O digest atual e o **histórico** de digests importados, independentemente do que acontecer no registry.
7. ImageStream no mesmo projeto, lookup local habilitado (`oc set image-lookup`) e referência pelo nome curto.
8. Os Deployments seguem o alias (ex.: `app:prod`) com trigger. Mover o alias para a versão testada promove; movê-lo de volta reverte, ambos com rollout automático.
9. `oc image info --filter-by-os linux/amd64 registry.access.redhat.com/ubi10/httpd-24:latest` (ou `skopeo inspect ... | jq -r .Digest`).
10. `oc set image deployment/site web=registry.access.redhat.com/ubi10/httpd-24:10.0`
11. `oc rollout pause deployment/site` → `oc set image ...` → `oc set env deployment/site MODO=prod` → `oc rollout resume deployment/site`
12. `oc rollout history deployment/site` e `oc rollout undo deployment/site --to-revision 3`
13. `oc import-image site:1.0 --from quay.io/exemplo/site:1.0 --confirm` (ou `oc tag quay.io/exemplo/site:1.0 site:1.0`).
14. `oc tag quay.io/exemplo/site:1.0 site:1.0 --scheduled`
15. `oc set image-lookup site` e `oc create deployment vitrine --image site:1.0`
16. `oc set triggers deployment/vitrine --from-image site:prod --containers site`
17. `oc tag --alias site:1.1 site:prod`
18. Uso de tag flutuante com `IfNotPresent`: nós diferentes têm imagens diferentes para a mesma tag. Prevenir com digest, tag estática ou ImageStream.
19. Com RollingUpdate, os Pods antigos continuam atendendo (o novo ReplicaSet não fica pronto) até o prazo de progresso estourar. O OpenShift não reverte sozinho: `oc rollout undo` e corrigir a imagem.
20. Não há image trigger no Deployment (ou está `--manual`); o Deployment está pausado; ou ele não usa a ImageStream (nome completo em vez do curto, IS em outro projeto ou sem lookup).

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 18–20 | Siga para o Capítulo 8 |
| 14–17 | Refaça a Parte C das lições onde errou |
| < 14 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
