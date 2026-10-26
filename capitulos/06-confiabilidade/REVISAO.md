# Revisão — Capítulo 6

Questões **autorais**. Elas não reproduzem o quiz oficial nem perguntas de exame.

## Parte 1 — Conceitos

1. Por que um Pod `Running` pode estar indisponível para usuários, e o que permite ao cluster perceber isso?
2. Compare startup, readiness e liveness: quando rodam e o que acontece quando falham.
3. Explique as três etapas do scheduler.
4. O que é allocatable e por que ele é menor que a capacidade do nó?
5. O que acontece quando um container atinge o limit de memória? E o de CPU?
6. Por que o HPA precisa de requests?
7. Qual a novidade do 4.22 sobre redimensionamento de Pods, e como ela se relaciona com o VPA?
8. Por que runtimes antigos podem sofrer `OOMKilled` no 4.22?

## Parte 2 — Comandos (escreva o comando)

9. Adicionar ao Deployment `web` uma readiness HTTP em `/ready`, porta 8080, a cada 5 s, tolerando 3 falhas.
10. Adicionar uma startup por TCP na porta 5432 ao Deployment `pg`, permitindo até 2 minutos de inicialização com período de 10 s.
11. Definir requests `cpu=250m,memory=256Mi` e limits `cpu=500m,memory=512Mi` no Deployment `api`.
12. Mostrar o motivo do último término do primeiro container do Pod `api-x`.
13. Mostrar requests e limits alocados no nó `worker-1`.
14. Criar um HPA para `api` entre 2 e 8 réplicas, alvo de 75% de CPU.
15. Mostrar o estado e os eventos do HPA `api`.
16. Aumentar no local o limit de CPU do container `app` do Pod `api-x` para `800m`.

## Parte 3 — Diagnóstico

17. Novas réplicas ficam `Pending` com `Insufficient memory`, mas o nó usa só 30% da memória. Explique e proponha ações.
18. Um Pod reinicia em loop logo após iniciar; os eventos mostram `Liveness probe failed`. A aplicação demora 60 s para subir. O que fazer?
19. Durante escalas, clientes recebem erros por alguns segundos. O que falta?
20. O HPA está criado, mas a coluna `TARGETS` mostra `<unknown>` há 30 minutos. Causa e correção?

---

<details>
<summary>Respostas comentadas</summary>

1. A aplicação pode estar travada ou sem dependências sem que o processo morra. Só **probes** (readiness/liveness) permitem que o cluster detecte e reaja.
2. Startup: só no início, até o primeiro sucesso; ao esgotar o limite, reinicia o container. Readiness: toda a vida; falhando, tira o Pod dos endpoints. Liveness: toda a vida, após a startup; falhando o suficiente, reinicia o container.
3. Filtrar (selector, recursos para os requests), priorizar (pontuação ponderada) e selecionar (maior nota; empate em round-robin). Sem nó elegível: `FailedScheduling`.
4. É o que sobra para Pods: capacidade menos reservas do sistema (`system-reserved`) e limiares de despejo. O OpenShift calcula as reservas automaticamente.
5. Memória: o OOM killer mata um processo (`OOMKilled`, exit 137) e o container é reiniciado. CPU: throttling, e o container fica mais lento sem morrer.
6. Porque calcula o uso como percentual do request de cada Pod.
7. O *in-place pod resize* é GA: muda requests e limits sem recriar o Pod (`--subresource resize`, `resizePolicy`). O VPA, no modo `InPlaceOrRecreate` (desde o 4.21), usa esse recurso.
8. Desde o 4.19 só existe cgroups v2; runtimes que não o entendem calculam errado a memória disponível e consomem demais.
9. `oc set probe deployment/web --readiness --get-url http://:8080/ready --period-seconds 5 --failure-threshold 3`
10. `oc set probe deployment/pg --startup --open-tcp 5432 --period-seconds 10 --failure-threshold 12`
11. `oc set resources deployment/api --requests cpu=250m,memory=256Mi --limits cpu=500m,memory=512Mi`
12. `oc get pod api-x -o jsonpath='{.status.containerStatuses[0].lastState.terminated.reason}'`
13. `oc describe node worker-1` (seção *Allocated resources*).
14. `oc autoscale deployment/api --min 2 --max 8 --cpu 75%`
15. `oc get hpa api` e `oc describe hpa api`.
16. `oc patch pod api-x --subresource resize --type merge -p '{"spec":{"containers":[{"name":"app","resources":{"limits":{"cpu":"800m"}}}]}}'`
17. O scheduler soma os **requests**, não o uso. Se os requests já ocupam o allocatable, nada mais cabe. Ações: revisar requests superestimados, reduzir réplicas ou adicionar capacidade.
18. A liveness mata a aplicação antes de ela subir. Adicione uma **startup probe** com folga (ex.: período 10 s × 9 falhas) ou ajuste o atraso inicial da liveness.
19. **Readiness probe**: sem ela, Pods novos recebem tráfego antes de estarem prontos.
20. Falta **request** para a métrica no Deployment. Adicione com `oc set resources`.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 18–20 | Siga para o Capítulo 7 |
| 14–17 | Refaça a Parte C das lições onde errou |
| < 14 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
