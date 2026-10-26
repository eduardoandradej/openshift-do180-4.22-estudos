# Prática oficial — Capítulo 2

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial, no `workstation`, como `student`.
> As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 2.2 | Guided Exercise | `cli-interfaces` | Não | p. 95–102 |
| 2.4 | Guided Exercise | `cli-resources` | Não | p. 113–122 |
| 2.6 | Guided Exercise | `cli-health` | Não | p. 137–144 |
| 2.7 | Lab | `cli-review` | **Sim** | p. 145–152 |
| 2.8 | Quiz | — (sem comando `lab`) | — | p. 153–155 |

Identificadores e avaliação verificados no PDF do Capítulo 2.

---

## 2.2 Guided Exercise: The Kubernetes and OpenShift Command-line Interfaces

| Campo | Valor |
|-------|-------|
| Seção | 2.2 |
| Tipo | Guided Exercise |
| Identificador `lab` | `cli-interfaces` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 95–102 |

**Competência praticada:** localizar na console o download do `oc`, obter um token
e entrar pela CLI com ele, entrar também pelo navegador (`--web`), comparar
`kubectl` e `oc` e identificar componentes principais do cluster pela CLI.

**Domine antes:** [2.1](2.1-interfaces-de-linha-de-comando.md): métodos de login,
tipos de usuário, comandos essenciais.

```bash
lab start cli-interfaces
lab finish cli-interfaces
```

**Pontos de atenção:**
- `oc` e `kubectl` já estão instalados no `workstation`: o objetivo é **saber onde** baixá-los, não instalar.
- Depois de cada login, confirme **quem** você é (`oc whoami`) antes de continuar.
- Compare a ajuda das duas CLIs procurando comandos que **só** existem no `oc`.
- Recursos de escopo de cluster exigem o usuário administrador. Observe a diferença de resultado entre os usuários.

---

## 2.4 Guided Exercise: Inspect Kubernetes Resources

| Campo | Valor |
|-------|-------|
| Seção | 2.4 |
| Tipo | Guided Exercise |
| Identificador `lab` | `cli-resources` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 113–122 |

**Competência praticada:** listar e explicar tipos de recurso; filtrar por escopo e
por grupo de API (core, `apps`, `config.openshift.io`); mostrar recursos em YAML e
JSON; extrair dados com filtros, JSONPath e custom columns. O `lab start` cria uma
aplicação de exemplo em um projeto próprio da atividade.

**Domine antes:** [2.3](2.3-inspecionar-recursos-kubernetes.md): `api-resources`,
`explain`, `-o`, `.items`, JSONPath × `jq`.

```bash
lab start cli-resources
lab finish cli-resources
```

**Pontos de atenção:**
- Confirme o projeto atual antes de consultar a aplicação de exemplo.
- Ao filtrar, saiba se você está olhando uma **lista** (`.items[...]`) ou **um objeto**.
- Use `oc explain` para entender cada campo que aparecer no YAML.
- Contar recursos com `-o name | wc -l` é um bom jeito de comparar filtros.

---

## 2.6 Guided Exercise: Assess the Health of an OpenShift Cluster

| Campo | Valor |
|-------|-------|
| Seção | 2.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `cli-health` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 137–144 |

**Competência praticada:** ver status e detalhes de operators; obter status, consumo
e eventos de Pods; obter informações de nós; ver logs e status de serviços systemd
do nó; ver eventos e alertas; coletar dados de depuração.

**Domine antes:** [2.5](2.5-avaliar-a-saude-do-cluster.md) inteira, em especial o
roteiro da Parte B.

```bash
lab start cli-health
lab finish cli-health
```

**Pontos de atenção:**
- Distinga `oc get clusteroperators` de `oc get operators`.
- Leia as conditions pelo **tipo** e lembre a lógica invertida (pressões = `False` é bom).
- Em `oc adm top pods`, observe o efeito de `-A`, `--sum` e `--containers`.
- Em Pods com vários containers, `oc exec` e `oc logs` exigem `-c`.
- `must-gather` pode demorar alguns minutos e gerar bastante dado.

---

## 2.7 Lab: Kubernetes and OpenShift Command-line Interfaces and APIs

| Campo | Valor |
|-------|-------|
| Seção | 2.7 |
| Tipo | Lab de fim de capítulo |
| Identificador `lab` | `cli-review` |
| Avaliação | **`lab grade cli-review`** |
| Referência | PDF p. 145–152 |

**Competência praticada (resumo autoral):** criar um projeto e entrar com usuários
diferentes; identificar versão do cluster, versões de API, campos de um objeto,
cluster operators e tipos de recurso por escopo e por grupo; consultar eventos,
conditions de Pod com `jq`, consumo de Pods e nós com `oc adm top`, capacidade e
allocatable de nó com JSONPath; coletar dados de depuração do cluster e de um
cluster operator em diretórios específicos, limitando o período.

**Domine antes:** as três lições do capítulo e a [revisão](REVISAO.md).

```bash
lab start cli-review
lab grade cli-review      # repita até todos os critérios ficarem PASS
lab finish cli-review
```

**Pontos de atenção:**
- O enunciado indica **diretórios de destino** exatos para a coleta: o `lab grade` depende deles.
- Atenção ao usuário correto em cada etapa (comum × administrador).
- Para limitar o período em `oc adm inspect`, use `--since`.
- Se um critério falhar, leia a mensagem do `grade`, corrija e rode o `grade` de novo.

---

## 2.8 Quiz: Kubernetes and OpenShift Command-line Interfaces and APIs

| Campo | Valor |
|-------|-------|
| Seção | 2.8 |
| Tipo | Quiz |
| Referência | PDF p. 153–155 |

Questões sobre grupos de API, campos de objetos, conditions de nós, opções do
`oc adm top` e extração de dados de nós e cluster operators. Responda **depois** do
lab 2.7, de preferência confirmando cada alternativa no terminal. As respostas não
são registradas aqui.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 2.5 Saúde do cluster](2.5-avaliar-a-saude-do-cluster.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
