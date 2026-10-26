# Estado do projeto

> Registro do estado real do repositório para continuar em sessões futuras.
> Atualize este arquivo ao concluir cada capítulo. As regras permanentes ficam no
> [CLAUDE.md](../CLAUDE.md).

**Última atualização:** 2026-10-26 (Capítulo 6 concluído)

## Situação por módulo

| Módulo | Status | PDF recebido | Observações |
|--------|--------|--------------|-------------|
| Estrutura do repositório | ✅ | — | Árvore completa, modelos, `.gitignore`, navegação |
| 00-comecar-aqui | ✅ | Cap. 0 (p. 1–14) | Integrado: objetivos, ambiente, comando `lab` |
| 01-fundamentos-essenciais | ✅ | — | 8 lições autorais |
| Capítulo 1 | ✅ validado | p. 15–82 | 4 lições + prática, revisão, resumo |
| Capítulo 2 | ✅ validado | p. 83–156 | 3 lições + prática, revisão, resumo |
| Capítulo 3 | ✅ validado | p. 157–226 | 3 lições + prática, revisão, resumo |
| Capítulo 4 | ✅ validado | p. 227–292 | 4 lições + prática, revisão, resumo (sem quiz) |
| Capítulo 5 | ✅ validado | p. 293–376 | 4 lições + prática, revisão, resumo (sem quiz) |
| Capítulo 6 | ✅ validado | p. 377–436 | 5 lições + prática, revisão, resumo |
| Capítulo 7 | ⏳ | não | Só o índice oficial |
| Capítulo 8 | ⏳ | não | Só o índice oficial |
| consulta-rapida | 🟡 | — | Cobre fundamentos + Caps. 1–6; ampliar a cada capítulo |
| Mapa EX280 | 🟡 | — | Objetivos públicos a conferir na página oficial do exame |

## Fatos verificados no PDF

- Material: `DO180-RHOCP4.22-en-1-20260730`, edição 1 (2026-07-30), 513 páginas.
- Cluster de laboratório: OpenShift 4.22, nó único `master01`, bare metal UPI, domínio `lab.example.com`.
- Comando `lab`: `start`/`finish` em todas as atividades; `grade` só em labs de fim de capítulo e comprehensive reviews.
- Capítulo 6: 6.1 (p. 378–379), 6.2 GE `reliability-ha` (p. 380–385), 6.3 (p. 386–390), 6.4 GE `reliability-probes` (p. 391–396), 6.5 (p. 397–400), 6.6 GE `reliability-requests` (p. 401–404), 6.7 (p. 405–411), 6.8 GE `reliability-limits` (p. 412–414), 6.9 (p. 415–419), 6.10 GE `reliability-autoscaling` (p. 420–425), 6.11 Lab `reliability-review` (p. 426–433, **com** `lab grade`), 6.12 Quiz (p. 434–435), 6.13 Summary (p. 436).
- Capítulo 5: 5.1 (p. 294–306), 5.2 GE `storage-configs` (p. 307–316), 5.3 (p. 317–327), 5.4 GE `storage-volumes` (p. 328–335), 5.5 (p. 336–341), 5.6 GE `storage-classes` (p. 342–348), 5.7 (p. 349–355), 5.8 GE `storage-statefulsets` (p. 356–362), 5.9 Lab `storage-review` (p. 363–375, **com** `lab grade`), 5.10 Summary (p. 376). Sem quiz.
- StorageClasses do laboratório: `nfs-storage` (padrão, arquivo) e `lvms-vg1` (LVM local, bloco).
- Capítulo 4: 4.1 (p. 228–239), 4.2 GE `deploy-newapp` (p. 240–244), 4.3 (p. 245–250), 4.4 GE `deploy-workloads` (p. 251–255), 4.5 (p. 256–264), 4.6 GE `deploy-services` (p. 265–270), 4.7 (p. 271–278), 4.8 GE `deploy-routes` (p. 279–284), 4.9 Lab `deploy-review` (p. 285–291, **com** `lab grade`), 4.10 Summary (p. 292). Sem quiz.
- Rede do laboratório: Pods `10.8.0.0/14` (host prefix 23), Services `172.30.0.0/16`.
- Capítulo 3: 3.1 (p. 158–168), 3.2 GE `pods-containers` (p. 169–176), 3.3 (p. 177–189), 3.4 GE `pods-images` (p. 190–200), 3.5 (p. 201–207), 3.6 GE `pods-troubleshooting` (p. 208–213), 3.7 Lab `pods-review` (p. 214–221, **com** `lab grade`), 3.8 Quiz (p. 222–225), 3.9 Summary (p. 226).
- Capítulo 2: 2.1 (p. 84–94), 2.2 GE `cli-interfaces` (p. 95–102), 2.3 (p. 103–112), 2.4 GE `cli-resources` (p. 113–122), 2.5 (p. 123–136), 2.6 GE `cli-health` (p. 137–144), 2.7 Lab `cli-review` (p. 145–152, **com** `lab grade`), 2.8 Quiz (p. 153–155), 2.9 Summary (p. 156).
- Capítulo 1: 1.1 (p. 16–19), 1.2 Matching (p. 20–21), 1.3 (p. 22–25), 1.4 Matching (p. 26–28), 1.5 (p. 29–33), 1.6 GE `intro-navigate` (p. 34–48), 1.7 (p. 49–55), 1.8 GE `intro-monitor` (p. 56–71), 1.9 Lab `intro-review` (p. 72–79, sem `lab grade` no PDF), 1.10 Quiz (p. 80–81), 1.11 Summary (p. 82).

## Fluxo de publicação

Por decisão do usuário, o conteúdo é publicado direto no branch `main` (material de estudo, sem deploy).

## Validação do Capítulo 6

- [x] Seções 6.1–6.13 representadas, na ordem.
- [x] Identificadores `reliability-ha`, `reliability-probes`, `reliability-requests`, `reliability-limits`, `reliability-autoscaling`, `reliability-review` e `lab grade` (só no 6.11) conferidos.
- [x] Correções/complementos: `memory=1Gi` (o PDF usa `1gi`, sufixo inválido); liveness/startup reiniciam o **container** (fonte externa); padrões das probes, fórmula e estabilização do HPA, QoS classes e `--cpu-percent` marcados como fonte externa.
- [x] Quiz e lab sem respostas nem valores específicos.
- [x] YAML validado; links e âncoras verificados.

## Validação do Capítulo 5

- [x] Seções 5.1–5.10 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `storage-configs`, `storage-volumes`, `storage-classes`, `storage-statefulsets`, `storage-review` e `lab grade` (só no 5.9) conferidos.
- [x] Complementos marcados como fonte externa: `subPath` sem atualização, `volumeDevices` para PVC em modo Block, labels dos PVCs de StatefulSet, `oc create secret docker-registry`.
- [x] YAML validado; links e âncoras verificados; valores de Secret fictícios.

## Validação do Capítulo 4

- [x] Seções 4.1–4.10 representadas, na ordem; ausência de quiz registrada.
- [x] Identificadores `deploy-newapp`, `deploy-workloads`, `deploy-services`, `deploy-routes`, `deploy-review` e `lab grade` (só no 4.9) conferidos.
- [x] Exemplo de Gateway API reescrito de forma coerente (o do PDF usa nomes de GatewayClass divergentes).
- [x] `spec.timeZone` de CronJob marcado como fonte externa.
- [x] YAML validado; links e âncoras verificados; sem credenciais.

## Validação do Capítulo 3

- [x] Seções 3.1–3.9 representadas, na ordem.
- [x] Identificadores `pods-containers`, `pods-images`, `pods-troubleshooting`, `pods-review` e `lab grade` (só no 3.7) conferidos.
- [x] Pequenas correções em relação ao PDF: `oc run <nome>` (sem `RESOURCE/`), `crictl images` (plural), `[*]` em JSONPath; aspas simples em `--env` com `$`.
- [x] YAML validado; links e âncoras verificados; sem credenciais nem respostas do quiz.

## Validação do Capítulo 2

- [x] Seções 2.1–2.9 representadas, na ordem.
- [x] Identificadores `cli-interfaces`, `cli-resources`, `cli-health`, `cli-review` e `lab grade` (só no 2.7) conferidos.
- [x] YAML validado; links e âncoras verificados por script.
- [x] Sem senhas, tokens reais, e-mail ou trechos extensos; quiz sem respostas.
- [x] Consulta rápida, glossário e troubleshooting ampliados.

## Validação do Capítulo 1

- [x] Todas as seções oficiais (1.1–1.11) representadas, na ordem.
- [x] Identificadores `lab` conferidos no PDF.
- [x] YAML dos fundamentos validado com parser.
- [x] Links relativos e âncoras verificados por script.
- [x] Sem senhas, e-mails, marca d'água ou trechos extensos do PDF.
- [x] Quiz oficial sem respostas reproduzidas.

## Pendências e assuntos a retomar

| Item | Quando |
|------|--------|
| Detalhar *in-place pod resize* (citado em 1.1) com a abordagem oficial | Ao receber o Cap. 6 |
| Confirmar identificadores `lab` e `lab grade` dos capítulos 2–8 | A cada capítulo |
| Conferir objetivos públicos do EX280 e atualizar `objetivos-de-aprendizagem.md` | Antes do Cap. 8 |
| Ampliar `consulta-rapida` com o conteúdo de cada capítulo | A cada capítulo |
| SCC e RBAC em profundidade (citados nos Caps. 2 e 3) | DO280 |
| Rollout, estratégias e rollback de Deployments | Cap. 7 |
| LimitRange e ResourceQuota (citados em 6.9) | DO280 |
| TLS em Routes (edge, passthrough, re-encrypt) em profundidade | DO280 |
| Criptografia do etcd e RBAC sobre Secrets | DO280 |

## Próximo passo

Aguardar o PDF do **Capítulo 7 — Manage Application Updates**.
