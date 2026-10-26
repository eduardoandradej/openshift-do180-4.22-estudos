# Prática oficial — Capítulo 7

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial, no `workstation`, como `student`.
> As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 7.2 | Guided Exercise | `updates-ids` | Não | p. 445–452 |
| 7.4 | Guided Exercise | `updates-rollout` | Não | p. 461–466 |
| 7.6 | Guided Exercise | `updates-imagestreams` | Não | p. 477–479 |
| 7.8 | Guided Exercise | `updates-triggers` | Não | p. 485–488 |
| 7.9 | Lab | `updates-review` | **Sim** | p. 489–493 |

Identificadores e avaliação verificados no PDF do Capítulo 7. O capítulo não tem quiz.

---

## 7.2 Guided Exercise: Container Image Identity and Tags

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `updates-ids` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 445–452 |

**Competência praticada:** atualizar uma aplicação para uma tag mais nova e encontrar
os hashes das imagens antiga e nova; inspecionar imagens; listar as imagens dos
containers nos nós; implantar usando tags ou digests.

**Domine antes:** [7.1](7.1-identidade-e-tags-de-imagens.md).

```bash
lab start updates-ids
lab finish updates-ids
```

**Pontos de atenção:**
- Em imagens multiarquitetura, `oc image info` exige `--filter-by-os`.
- No nó, `crictl images --digests --no-trunc` mostra o digest completo; não confunda com `IMAGE ID`.
- Compare o `imageID` dos Pods antes e depois da atualização.

---

## 7.4 Guided Exercise: Update Application Image and Settings

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `updates-rollout` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 461–466 |

**Competência praticada:** atualizar os manifestos de um banco e de uma aplicação web
(com várias réplicas) minimizando a interrupção: pausar, alterar a configuração,
retomar e fazer rollback.

**Domine antes:** [7.3](7.3-atualizar-imagem-e-configuracoes.md).

```bash
lab start updates-rollout
lab finish updates-rollout
```

**Pontos de atenção:**
- O `lab start` deixa um arquivo de apoio com nomes de imagens e comandos no diretório da atividade.
- Use `oc rollout status` e `oc get replicaset` em paralelo para ver a troca.
- Um rollout que não progride não se reverte sozinho.

---

## 7.6 Guided Exercise: Reproducible Deployments with OpenShift Image Streams

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `updates-imagestreams` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 477–479 |

**Competência praticada:** criar ImageStreams e ImageStreamTags e implantar
aplicações que as referenciam indiretamente.

**Domine antes:** [7.5](7.5-implantacoes-reproduziveis-com-imagestreams.md).

```bash
lab start updates-imagestreams
lab finish updates-imagestreams
```

**Pontos de atenção:**
- Sem lookup local, o nome curto não é resolvido.
- `oc describe is` mostra a origem, o digest atual (`*`) e o histórico.

---

## 7.8 Guided Exercise: Automatic Image Updates with OpenShift Image Change Triggers

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `updates-triggers` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 485–488 |

**Competência praticada:** adicionar um image trigger a um Deployment com várias
réplicas, apontar a ImageStreamTag para uma imagem nova, acompanhar o rollout e
voltar para a imagem anterior.

**Domine antes:** [7.7](7.7-triggers-de-mudanca-de-imagem.md).

```bash
lab start updates-triggers
lab finish updates-triggers
```

**Pontos de atenção:**
- O trigger é por **container**: confira o nome com `oc get deployment -o wide`.
- O rollback é feito **pela tag**, não pelo `oc rollout undo`.

---

## 7.9 Lab: Manage Application Updates

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `updates-review` |
| Avaliação | **`lab grade updates-review`** |
| Referência | PDF p. 489–493 |

**Competência praticada (resumo autoral):** trocar uma tag flutuante por uma tag
estática em um Deployment; habilitar image trigger em outro Deployment que usa um
alias de ImageStreamTag; criar uma ImageStreamTag para uma versão nova aprovada e
mover o alias para ela, verificando o rollout.

**Domine antes:** as quatro lições e a [revisão](REVISAO.md).

```bash
lab start updates-review
lab grade updates-review
lab finish updates-review
```

**Pontos de atenção:**
- Identifique o **nome do container** antes de `oc set image` e `oc set triggers`.
- Crie a nova istag **antes** de mover o alias.
- Confirme o rollout com `oc rollout status` e o digest dos Pods.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 7.7 Triggers](7.7-triggers-de-mudanca-de-imagem.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
