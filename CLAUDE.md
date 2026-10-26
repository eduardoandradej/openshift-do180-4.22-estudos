# CLAUDE.md — Regras permanentes do projeto

Este arquivo orienta qualquer sessão futura do Claude Code neste repositório.
Leia-o inteiro antes de criar ou alterar conteúdo.

## 1. Propósito

Guia pessoal de estudos do curso **Red Hat OpenShift Administration I: Operating a
Production Cluster (DO180), versão 4.22** (OpenShift Container Platform 4.22,
Kubernetes 1.35). Objetivo final: base sólida para DO280 e para o exame EX280.

O repositório **não é uma tradução** da apostila. É material autoral: explicações
próprias, exemplos originais, revisões e ponte para os laboratórios oficiais.

## 2. Regras de conteúdo (obrigatórias)

- Texto didático em **português brasileiro**; nomes técnicos, comandos, campos YAML,
  recursos e objetos Kubernetes/OpenShift permanecem em **inglês**.
- Respeitar a **cronologia e a numeração oficial** de capítulos e seções.
- **Não** traduzir capítulos ou exercícios integralmente; **não** copiar parágrafos
  extensos, figuras, tabelas proprietárias, enunciados, soluções ou gabaritos
  (inclusive respostas de quizzes oficiais).
- **Não** versionar o PDF, extrações de texto, credenciais, tokens, kubeconfigs,
  dados da assinatura, nomes de usuário/e-mail que aparecem na marca d'água do PDF
  nem senhas do ambiente de laboratório.
- Referências a páginas do PDF somente após verificação, no formato `PDF p. NN`.
- Identificadores de `lab` somente se verificados no PDF. Nunca inventar.
- `lab grade` apenas quando a atividade oficial aceitar avaliação.
- Conteúdo de documentação pública deve ser marcado como fonte externa.
- Não presumir que comportamentos de versões anteriores valem para 4.22.
- Regra central: **simplificar a explicação, nunca simplificar incorretamente a tecnologia.**

## 3. Formato das lições

Toda lição conceitual segue `modelos/modelo-licao.md`:
Identificação → Partes A (conceito), B (modelo mental), C (prática), D (relações),
E (preparação para o lab), F (fixação com respostas recolhíveis), G (essencial).
Cada lição termina com a barra de navegação `Anterior | Índice do capítulo | Próximo`.

Cada capítulo em `capitulos/NN-nome/` contém:
`README.md` (índice), um arquivo por seção conceitual (`N.M-titulo.md`),
`PRATICA-OFICIAL.md`, `REVISAO.md`, `RESUMO.md`.

## 4. Proibições operacionais

- Não executar exercícios oficiais nem criar scripts que reproduzam ou alterem a
  infraestrutura do treinamento.
- Não criar avaliadores próprios dos laboratórios.
- Não tornar o repositório público em nenhuma hipótese.
- O `.gitignore` bloqueia `*.pdf`, `*token*`, `*secret*.yaml` etc. Exemplos de
  Secret devem ficar dentro de Markdown com valores fictícios.

## 5. Fluxo de trabalho por capítulo

1. O usuário envia o PDF (ou trecho) do capítulo; extrair texto apenas no scratchpad,
   nunca dentro do repositório.
2. Confirmar seções, páginas e identificadores `lab`.
3. Produzir as lições seção por seção; depois PRATICA-OFICIAL, REVISAO, RESUMO.
4. Controle de qualidade (seção 10 do prompt mestre): cobertura das seções, ordem,
   precisão de comandos, YAML válido, português revisado, sem transcrição.
5. Atualizar `progresso/checklist-geral.md`, `progresso/objetivos-de-aprendizagem.md`,
   a tabela de status abaixo e o README do capítulo.
6. Commit organizado e push no branch de trabalho.

## 6. Metodologia incremental (decisão do usuário)

- **Um capítulo por vez.** Cada capítulo é fornecido em PDF separado. Não antecipar
  capítulos cujo PDF ainda não foi recebido: os READMEs dos capítulos 2–8 contêm
  apenas o índice oficial.
- Antes de iniciar um capítulo: ler este arquivo, `progresso/estado-do-projeto.md`,
  a estrutura existente e os capítulos concluídos. Preservar padrão, navegação e links.
- Não recriar nem sobrescrever conteúdo anterior sem necessidade comprovada.
- Prioridade: um capítulo bem desenvolvido e correto vale mais que vários superficiais.
- Capítulo 0 (introdução do curso) alimenta `00-comecar-aqui/`, sem refazer capítulos.

## 7. Estado do projeto

O estado efetivo (capítulos concluídos, fatos verificados no PDF, pendências e
próximo passo) fica em **[progresso/estado-do-projeto.md](progresso/estado-do-projeto.md)**.
Atualize-o ao final de cada capítulo.
