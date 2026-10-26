# Estado do projeto

> Registro do estado real do repositório para continuar em sessões futuras.
> Atualize este arquivo ao concluir cada capítulo. As regras permanentes ficam no
> [CLAUDE.md](../CLAUDE.md).

**Última atualização:** 2026-10-26

## Situação por módulo

| Módulo | Status | PDF recebido | Observações |
|--------|--------|--------------|-------------|
| Estrutura do repositório | ✅ | — | Árvore completa, modelos, `.gitignore`, navegação |
| 00-comecar-aqui | ✅ | Cap. 0 (p. 1–14) | Integrado: objetivos, ambiente, comando `lab` |
| 01-fundamentos-essenciais | ✅ | — | 8 lições autorais |
| Capítulo 1 | ✅ validado | p. 15–82 | 4 lições + prática, revisão, resumo |
| Capítulo 2 | ⏳ | não | Só o índice oficial (sumário p. 3) |
| Capítulo 3 | ⏳ | não | Só o índice oficial |
| Capítulo 4 | ⏳ | não | Só o índice oficial |
| Capítulo 5 | ⏳ | não | Só o índice oficial |
| Capítulo 6 | ⏳ | não | Só o índice oficial |
| Capítulo 7 | ⏳ | não | Só o índice oficial |
| Capítulo 8 | ⏳ | não | Só o índice oficial |
| consulta-rapida | 🟡 | — | Cobre fundamentos + Cap. 1; ampliar a cada capítulo |
| Mapa EX280 | 🟡 | — | Objetivos públicos a conferir na página oficial do exame |

## Fatos verificados no PDF

- Material: `DO180-RHOCP4.22-en-1-20260730`, edição 1 (2026-07-30), 513 páginas.
- Cluster de laboratório: OpenShift 4.22, nó único `master01`, bare metal UPI, domínio `lab.example.com`.
- Comando `lab`: `start`/`finish` em todas as atividades; `grade` só em labs de fim de capítulo e comprehensive reviews.
- Capítulo 1: 1.1 (p. 16–19), 1.2 Matching (p. 20–21), 1.3 (p. 22–25), 1.4 Matching (p. 26–28), 1.5 (p. 29–33), 1.6 GE `intro-navigate` (p. 34–48), 1.7 (p. 49–55), 1.8 GE `intro-monitor` (p. 56–71), 1.9 Lab `intro-review` (p. 72–79, sem `lab grade` no PDF), 1.10 Quiz (p. 80–81), 1.11 Summary (p. 82).

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
| Conferir no Cap. 2 se os comandos de CLI citados na lição 1.7 (`oc adm node-logs`, `oc adm top`) aparecem com a mesma sintaxe | Ao receber o Cap. 2 |
| Detalhar *in-place pod resize* (citado em 1.1) com a abordagem oficial | Ao receber o Cap. 6 |
| Confirmar identificadores `lab` e `lab grade` dos capítulos 2–8 | A cada capítulo |
| Conferir objetivos públicos do EX280 e atualizar `objetivos-de-aprendizagem.md` | Antes do Cap. 8 |
| Ampliar `consulta-rapida` com o conteúdo de cada capítulo | A cada capítulo |

## Próximo passo

Aguardar o PDF do **Capítulo 2 — Kubernetes and OpenShift Command-line Interfaces and APIs**.
