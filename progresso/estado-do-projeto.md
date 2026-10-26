# Estado do projeto

> Registro do estado real do repositório para continuar em sessões futuras.
> Atualize este arquivo ao concluir cada capítulo. As regras permanentes ficam no
> [CLAUDE.md](../CLAUDE.md).

**Última atualização:** 2026-10-26 (Capítulo 2 concluído)

## Situação por módulo

| Módulo | Status | PDF recebido | Observações |
|--------|--------|--------------|-------------|
| Estrutura do repositório | ✅ | — | Árvore completa, modelos, `.gitignore`, navegação |
| 00-comecar-aqui | ✅ | Cap. 0 (p. 1–14) | Integrado: objetivos, ambiente, comando `lab` |
| 01-fundamentos-essenciais | ✅ | — | 8 lições autorais |
| Capítulo 1 | ✅ validado | p. 15–82 | 4 lições + prática, revisão, resumo |
| Capítulo 2 | ✅ validado | p. 83–156 | 3 lições + prática, revisão, resumo |
| Capítulo 3 | ⏳ | não | Só o índice oficial |
| Capítulo 4 | ⏳ | não | Só o índice oficial |
| Capítulo 5 | ⏳ | não | Só o índice oficial |
| Capítulo 6 | ⏳ | não | Só o índice oficial |
| Capítulo 7 | ⏳ | não | Só o índice oficial |
| Capítulo 8 | ⏳ | não | Só o índice oficial |
| consulta-rapida | 🟡 | — | Cobre fundamentos + Caps. 1–2; ampliar a cada capítulo |
| Mapa EX280 | 🟡 | — | Objetivos públicos a conferir na página oficial do exame |

## Fatos verificados no PDF

- Material: `DO180-RHOCP4.22-en-1-20260730`, edição 1 (2026-07-30), 513 páginas.
- Cluster de laboratório: OpenShift 4.22, nó único `master01`, bare metal UPI, domínio `lab.example.com`.
- Comando `lab`: `start`/`finish` em todas as atividades; `grade` só em labs de fim de capítulo e comprehensive reviews.
- Capítulo 2: 2.1 (p. 84–94), 2.2 GE `cli-interfaces` (p. 95–102), 2.3 (p. 103–112), 2.4 GE `cli-resources` (p. 113–122), 2.5 (p. 123–136), 2.6 GE `cli-health` (p. 137–144), 2.7 Lab `cli-review` (p. 145–152, **com** `lab grade`), 2.8 Quiz (p. 153–155), 2.9 Summary (p. 156).
- Capítulo 1: 1.1 (p. 16–19), 1.2 Matching (p. 20–21), 1.3 (p. 22–25), 1.4 Matching (p. 26–28), 1.5 (p. 29–33), 1.6 GE `intro-navigate` (p. 34–48), 1.7 (p. 49–55), 1.8 GE `intro-monitor` (p. 56–71), 1.9 Lab `intro-review` (p. 72–79, sem `lab grade` no PDF), 1.10 Quiz (p. 80–81), 1.11 Summary (p. 82).

## Fluxo de publicação

Por decisão do usuário, o conteúdo é publicado direto no branch `main` (material de estudo, sem deploy).

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
| `oc debug`, `oc logs --previous`, `oc exec`/`oc rsh`: aprofundar com o enfoque oficial | Ao receber o Cap. 3 (seção 3.5) |
| Políticas de segurança que impedem execução como root (citadas em 2.5 com `--as-user`) | Cap. 3 |

## Próximo passo

Aguardar o PDF do **Capítulo 3 — Run Applications as Containers and Pods**.
