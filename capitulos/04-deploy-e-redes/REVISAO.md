# Revisão — Capítulo 4

Questões **autorais**. Elas não reproduzem atividades oficiais nem perguntas de exame.

## Parte 1 — Conceitos

1. Por que, em Kubernetes, é mais preciso falar em "recursos" do que em "aplicação"?
2. Diferencie gerenciamento imperativo e declarativo com um exemplo de cada.
3. O que `oc new-app` faz de diferente de `oc create deployment`?
4. Quando escolher Job, CronJob, Deployment, DaemonSet e StatefulSet?
5. Por que um frontend não deve usar o IP do Pod do backend?
6. Explique `port` × `targetPort` em um Service.
7. Qual a relação entre Ingress e Route no OpenShift?
8. Liste os três recursos da Gateway API e o escopo de cada um.

## Parte 2 — Comandos (escreva o comando)

9. Listar os parâmetros do template `postgresql-persistent` do projeto `openshift`.
10. Criar a aplicação a partir desse template, com `POSTGRESQL_DATABASE=vendas` e `DATABASE_SERVICE_NAME=pg`.
11. Gerar, sem criar nada, o YAML de um Deployment `api` com a imagem `registry.access.redhat.com/ubi10/httpd-24`.
12. Criar um CronJob `limpeza` que roda `date` todo dia às 03:00.
13. Criar um Service `api` para o Deployment `api`, escutando na porta 80 e encaminhando para a 8080.
14. Listar os endpoints do Service `api`.
15. Expor o Service `api` com o hostname `api.apps.exemplo.com`.
16. Escalar o Deployment `api` para 4 réplicas.
17. Criar um Ingress `api-ing` para `api.apps.exemplo.com/*` apontando para `api:80`.

## Parte 3 — Diagnóstico

18. A Route responde 503. Liste a sequência de verificações.
19. O Pod `web` não resolve o nome `db`, mas o Service `db` existe no projeto `dados`. Explique e corrija.
20. Você escalou para 3 réplicas, mas o EndpointSlice mostra só 1 IP. Cite causas possíveis.

---

<details>
<summary>Respostas comentadas</summary>

1. O termo "aplicação" é ambíguo (sistema ou serviço). O Kubernetes gerencia um conjunto de recursos (Deployment, Service, PVC...) que, juntos, formam o que chamamos de aplicação.
2. Imperativo: `oc create deployment web --image ...` (uma ordem). Declarativo: `oc apply -f web.yaml` (um estado desejado, versionável).
3. `oc new-app` usa heurística para criar vários recursos a partir de imagem, Git, template ou arquivo (ImageStream, Deployment, Service, BuildConfig...); `oc create deployment` cria só o Deployment.
4. Job: tarefa única até concluir. CronJob: tarefa recorrente. Deployment: serviço stateless contínuo. DaemonSet: um Pod por nó. StatefulSet: réplicas com identidade e storage próprios.
5. O IP do Pod muda quando ele é recriado; o Service oferece IP e nome estáveis, além de balanceamento.
6. `port` é a porta em que o Service escuta; `targetPort` é a porta do container para onde o tráfego vai.
7. O OpenShift converte cada Ingress em uma Route gerenciada (removida junto com o Ingress). Routes são preferidas pelos recursos extras.
8. GatewayClass (cluster), Gateway (namespace) e HTTPRoute (namespace).
9. `oc process --parameters postgresql-persistent -n openshift` (ou `oc describe template postgresql-persistent -n openshift`).
10. `oc new-app --template postgresql-persistent --param POSTGRESQL_DATABASE=vendas --param DATABASE_SERVICE_NAME=pg`
11. `oc create deployment api --image registry.access.redhat.com/ubi10/httpd-24 --dry-run=client -o yaml`
12. `oc create cronjob limpeza --image registry.access.redhat.com/ubi9/ubi --schedule "0 3 * * *" -- date`
13. `oc expose deployment/api --port 80 --target-port 8080`
14. `oc get endpointslices -l kubernetes.io/service-name=api`
15. `oc expose service api --hostname api.apps.exemplo.com`
16. `oc scale --replicas=4 deployment/api`
17. `oc create ingress api-ing --rule="api.apps.exemplo.com/*=api:80"`
18. `oc get route` (host e Service corretos?) → `oc get svc` e `oc describe svc` (seletor e portas) → `oc get endpointslices` (há endpoints?) → `oc get pods --show-labels` (labels e `READY`) → `oc logs` (a aplicação escuta na porta?) → `oc port-forward` direto ao Pod para isolar.
19. Sem sufixo, o nome `db` só resolve para Services do **mesmo** projeto. Use `db.dados` (ou o FQDN `db.dados.svc.cluster.local`).
20. Duas réplicas não estão prontas (`Ready` em `False`, ainda iniciando ou falhando); ou os Pods novos não têm o label do seletor; ou não foram agendados (`Pending`).

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 18–20 | Siga para o Capítulo 5 |
| 14–17 | Refaça a Parte C das lições onde errou |
| < 14 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
