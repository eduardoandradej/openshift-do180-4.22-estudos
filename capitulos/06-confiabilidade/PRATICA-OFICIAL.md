# Prática oficial — Capítulo 6

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial, no `workstation`, como `student`.
> As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 6.2 | Guided Exercise | `reliability-ha` | Não | p. 380–385 |
| 6.4 | Guided Exercise | `reliability-probes` | Não | p. 391–396 |
| 6.6 | Guided Exercise | `reliability-requests` | Não | p. 401–404 |
| 6.8 | Guided Exercise | `reliability-limits` | Não | p. 412–414 |
| 6.10 | Guided Exercise | `reliability-autoscaling` | Não | p. 420–425 |
| 6.11 | Lab | `reliability-review` | **Sim** | p. 426–433 |
| 6.12 | Quiz | — (sobre o lab 6.11) | — | p. 434–435 |

Identificadores e avaliação verificados no PDF do Capítulo 6.

> Vários exercícios usam uma imagem de treinamento com **endpoints utilitários**
> (derrubar o processo, alternar o estado de saúde, consumir memória). Use-os para
> **observar** cada mecanismo antes e depois da configuração.

---

## 6.2 Guided Exercise: Application High Availability with Kubernetes

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `reliability-ha` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 380–385 |

**Competência praticada:** simular falhas e observar a reação do Kubernetes: o efeito
da `restartPolicy` em Pods que caem, o comportamento de uma aplicação de
inicialização lenta **sem probes** e o que acontece com o tráfego quando uma réplica
de um Deployment "quebra".

**Domine antes:** [6.1](6.1-alta-disponibilidade-de-aplicacoes.md).

```bash
lab start reliability-ha
lab finish reliability-ha
```

**Pontos de atenção:**
- Acompanhe `STATUS` e `RESTARTS` com `oc get pods -w` em um terminal separado.
- Observe que o Pod "doente" continua `Running` e recebendo tráfego: é a motivação para as probes.

---

## 6.4 Guided Exercise: Application Health Probes

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `reliability-probes` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 391–396 |

**Competência praticada:** avaliar os problemas de uma aplicação sem probes e
configurar probes de **startup**, **liveness** e **readiness**, verificando que os
clientes ficam isolados das falhas.

**Domine antes:** [6.3](6.3-health-probes.md) (tipos, testes, tempos, `oc set probe`).

```bash
lab start reliability-probes
lab finish reliability-probes
```

**Pontos de atenção:**
- Ajuste os tempos ao tempo real de inicialização da aplicação.
- Confirme cada probe com `oc describe deployment` e os efeitos com eventos `Unhealthy`.
- Readiness falhando: `READY 0/1` e o Pod fora dos endpoints, sem reinício.

---

## 6.6 Guided Exercise: Reserving Compute Capacity for Applications

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `reliability-requests` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 401–404 |

**Competência praticada:** ver como requests de memória consomem a memória alocável
do nó e como ajustá-los muda o número de réplicas agendáveis.

**Domine antes:** [6.5](6.5-reservar-capacidade-de-computacao.md).

```bash
lab start reliability-requests
lab finish reliability-requests
```

**Pontos de atenção:**
- Faça a conta antes: allocatable − requests já alocados ÷ request por réplica.
- Réplicas que não cabem ficam `Pending` com `FailedScheduling`.
- O uso real (`oc adm top`) não muda a conta do scheduler.

---

## 6.8 Guided Exercise: Limit Compute Capacity for Applications

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `reliability-limits` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 412–414 |

**Competência praticada:** monitorar o uso de memória de uma aplicação e definir um
limit de memória para o Pod, observando o que acontece ao ultrapassá-lo.

**Domine antes:** [6.7](6.7-limitar-capacidade-de-computacao.md).

```bash
lab start reliability-limits
lab finish reliability-limits
```

**Pontos de atenção:**
- O `lab start` deixa um arquivo de apoio com comandos no diretório da atividade.
- Procure `OOMKilled` em `Last State` e o aumento de `RESTARTS`.

---

## 6.10 Guided Exercise: Application Autoscaling

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `reliability-autoscaling` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 420–425 |

**Competência praticada:** implantar uma aplicação, escalá-la manualmente, configurar
requests, criar um HPA e observar a escala sob teste de carga.

**Domine antes:** [6.9](6.9-autoscaling-de-aplicacoes.md).

```bash
lab start reliability-autoscaling
lab finish reliability-autoscaling
```

**Pontos de atenção:**
- Sem requests, o HPA mostra `<unknown>`.
- As métricas podem levar alguns minutos para aparecer; use `watch oc get hpa`.
- A redução de réplicas após a carga é mais lenta que o aumento.

---

## 6.11 Lab: Configure an Application for Reliability

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `reliability-review` |
| Avaliação | **`lab grade reliability-review`** |
| Referência | PDF p. 426–433 |

**Competência praticada (resumo autoral):** diagnosticar e corrigir uma aplicação que
não inicia por causa da configuração de recursos; configurar uma probe para que
réplicas novas só recebam tráfego quando prontas; e criar um HPA baseado em
**memória** com nome, mínimo, máximo e alvo definidos.

**Domine antes:** as cinco lições e a [revisão](REVISAO.md).

```bash
lab start reliability-review
lab grade reliability-review
lab finish reliability-review
```

**Pontos de atenção:**
- Comece pelo **evento** do Pod que não inicia: ele diz em que etapa está o problema (agendamento × execução).
- Compare requests com o allocatable do nó.
- Escolha o tipo de probe que **remove o Pod do tráfego** enquanto ele inicializa.
- O arquivo de exemplo de HPA fornecido está **incompleto**: use `oc explain` para os campos de `target`.
- Nomes e valores pedidos são conferidos pelo `lab grade`.

---

## 6.12 Quiz: Configure an Application for Reliability

| Campo | Valor |
|-------|-------|
| Tipo | Quiz sobre o lab 6.11 |
| Referência | PDF p. 434–435 |

As perguntas tratam das configurações encontradas e corrigidas no lab: quantos Pods
cabem no nó, qual configuração impedia a inicialização, o que faltava sem impedir a
execução e qual métrica e alvo o HPA usa. Responda **depois** do lab. As respostas
não são registradas aqui.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 6.9 Autoscaling](6.9-autoscaling-de-aplicacoes.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
