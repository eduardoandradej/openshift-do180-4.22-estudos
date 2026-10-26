# Prática oficial — Capítulo 1

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial da Red Hat, no `workstation`, como
> usuário `student`. As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 1.2 | Matching | — (sem comando `lab`) | — | p. 20–21 |
| 1.4 | Matching | — (sem comando `lab`) | — | p. 26–28 |
| 1.6 | Guided Exercise | `intro-navigate` | Não | p. 34–48 |
| 1.8 | Guided Exercise | `intro-monitor` | Não | p. 56–71 |
| 1.9 | Lab | `intro-review` | Não aparece no PDF: o resultado é conferido pelo quiz 1.10 | p. 72–79 |
| 1.10 | Quiz | — (usa o ambiente do `intro-review`) | — | p. 80–81 |

Identificadores verificados no PDF do Capítulo 1.

---

## 1.2 Matching: Containers and Kubernetes

| Campo | Valor |
|-------|-------|
| Seção | 1.2 |
| Tipo | Matching (associação conceito ↔ descrição) |
| Referência | PDF p. 20–21 |

**Competência praticada:** reconhecer as capacidades do Kubernetes e os conceitos
de imagem e gerenciamento declarativo a partir de descrições curtas.

**Domine antes:** a tabela de capacidades da [lição 1.1](1.1-containers-e-kubernetes.md#as-capacidades-que-o-kubernetes-oferece).

**Pontos de atenção:** diferencie bem escala **horizontal** (número de réplicas)
de **vertical** (CPU/memória de Pods em execução), e *self-healing* (recuperar) de
*automated rollout* (gerenciar versões).

---

## 1.4 Matching: Red Hat OpenShift Components and Editions

| Campo | Valor |
|-------|-------|
| Seção | 1.4 |
| Tipo | Matching |
| Referência | PDF p. 26–28 |

**Competência praticada:** situar Kubernetes, edições do OpenShift, RHEL CoreOS,
Lightspeed advisor, EUS e soberania digital.

**Domine antes:** [lição 1.3](1.3-componentes-e-edicoes-do-openshift.md).

**Pontos de atenção:** qual edição inclui um **registry** (Quay); o que distingue
**cloud services** de **self-managed**; qual serviço fica no **Hybrid Cloud
Console**.

---

## 1.6 Guided Exercise: Navigate the OpenShift Web Console

| Campo | Valor |
|-------|-------|
| Seção | 1.6 |
| Tipo | Guided Exercise |
| Identificador `lab` | `intro-navigate` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 34–48 |

**Competência praticada:** chegar à console a partir da CLI, trabalhar como
**desenvolvedor** (criar projeto, implantar uma aplicação de exemplo a partir de um
repositório Git interno e examinar os objetos gerados) e depois como
**administrador** (inspecionar Operators instalados e workloads e serviços de todo o
cluster).

**Domine antes:**
- [1.5 — Web console](1.5-navegar-na-web-console.md): URL da console, perspectiva unificada, menus.
- [F4 — Pods e workloads](../../01-fundamentos-essenciais/04-pods-e-workloads.md) e [F6 — Redes e serviços](../../01-fundamentos-essenciais/06-redes-e-servicos.md): o que são Deployment, Pod, Service e Route.

**Comandos administrativos:**

```bash
lab start intro-navigate
lab finish intro-navigate
```

**Pontos de atenção (sem spoilers):**
- Observe **quais objetos** a ação de implantação criou e **como se ligam**
  (Deployment → Pod; Service → Pod; Route → Service).
- Compare a quantidade de itens em *Pods* e *Services* vista pelo desenvolvedor e
  pelo administrador. A diferença é a autorização, não um erro.
- Como administrador, **não altere nem remova** componentes do cluster.
- O botão de criação só é liberado depois que a console valida o repositório Git.
- Pode levar alguns minutos até o Pod da aplicação ficar pronto.

---

## 1.8 Guided Exercise: Monitor an OpenShift Cluster

| Campo | Valor |
|-------|-------|
| Seção | 1.8 |
| Tipo | Guided Exercise |
| Identificador `lab` | `intro-monitor` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 56–71 |

**Competência praticada:** avaliar o estado geral do cluster pela página Overview;
abrir um terminal no nó e verificar os serviços `kubelet` e `crio`; explorar
alertas, regras de alerta e métricas; filtrar eventos.

**Domine antes:**
- [1.7 — Monitorar um cluster](1.7-monitorar-um-cluster-openshift.md): debug pod, `chroot /host`, métricas × alertas × eventos.
- [F2 — Arquitetura Kubernetes](../../01-fundamentos-essenciais/02-arquitetura-kubernetes.md): por que kubelet e CRI-O são serviços do sistema operacional do nó.

**Comandos administrativos:**

```bash
lab start intro-monitor
lab finish intro-monitor
```

**Comandos que você usará dentro do terminal do nó (conceito na lição 1.7):**
`chroot /host`, `systemctl status kubelet`, `systemctl status crio` (`q` sai do
paginador).

**Pontos de atenção:**
- O cluster de treinamento tem **um único nó** (`master01`), que acumula control plane e compute.
- Ao abrir uma regra de alerta, leia a **descrição** e a **expressão** (PromQL) para entender o que ela mede.
- A página de eventos pode demorar para popular. Combine filtros de **recurso**, **tipo** e **texto**.

---

## 1.9 Lab: Introduction to Kubernetes and OpenShift

| Campo | Valor |
|-------|-------|
| Seção | 1.9 |
| Tipo | Lab (de fim de capítulo) |
| Identificador `lab` | `intro-review` |
| Avaliação | O PDF **não** mostra `lab grade` nesta atividade; as respostas são conferidas no quiz 1.10 |
| Referência | PDF p. 72–79 |

**Competência praticada:** localizar informações de configuração do cluster pela
console: versão do cluster, severidades de alerta, labels de uma Route da
plataforma, StorageClasses e Operators instalados.

**Domine antes:**
- Mapa de navegação da [lição 1.5](1.5-navegar-na-web-console.md#mapa-da-navegação-lateral-o-que-usar-no-do180).
- Alerting e Overview da [lição 1.7](1.7-monitorar-um-cluster-openshift.md).
- StorageClass em [F7](../../01-fundamentos-essenciais/07-persistencia-de-dados.md).

**Comandos administrativos:**

```bash
lab start intro-review
lab finish intro-review     # somente depois de responder o quiz 1.10
```

**Pontos de atenção:**
- Para ver Operators de todo o cluster, verifique se o seletor de projeto está em **All Projects**.
- Routes da plataforma ficam em namespaces `openshift-*`. Use a busca da lista.
- Desafio extra (opcional, autoral): confirme cada informação também pela CLI
  (`oc get clusterversion`, `oc get storageclass`, `oc get route -A`,
  `oc get csv -A`). Isso antecipa o Capítulo 2.

---

## 1.10 Quiz: Introduction to Kubernetes and OpenShift

| Campo | Valor |
|-------|-------|
| Seção | 1.10 |
| Tipo | Quiz baseado nas observações do lab 1.9 |
| Referência | PDF p. 80–81 |

Responda **com o ambiente do `intro-review` ativo**, consultando a console. As
respostas não são registradas aqui de propósito: elas dependem do que você
observar no cluster.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 1.7 Monitorar um cluster](1.7-monitorar-um-cluster-openshift.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
