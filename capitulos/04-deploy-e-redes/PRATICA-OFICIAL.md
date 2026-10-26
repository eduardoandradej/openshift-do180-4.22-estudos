# Prática oficial — Capítulo 4

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial, no `workstation`, como `student`.
> As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 4.2 | Guided Exercise | `deploy-newapp` | Não | p. 240–244 |
| 4.4 | Guided Exercise | `deploy-workloads` | Não | p. 251–255 |
| 4.6 | Guided Exercise | `deploy-services` | Não | p. 265–270 |
| 4.8 | Guided Exercise | `deploy-routes` | Não | p. 279–284 |
| 4.9 | Lab | `deploy-review` | **Sim** | p. 285–291 |

Identificadores e avaliação verificados no PDF do Capítulo 4. O capítulo não tem quiz.

---

## 4.2 Guided Exercise: Deploy Applications from an Image and from a Template

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `deploy-newapp` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 240–244 |

**Competência praticada:** implantar um banco de dados a partir de uma imagem e a
partir de um template pela CLI, e comparar os recursos e atributos que cada método gera.

**Domine antes:** [4.1](4.1-implantar-a-partir-de-imagem-e-template.md):
`oc new-app`, templates, `oc process`, `all` × tipos que ficam de fora.

```bash
lab start deploy-newapp
lab finish deploy-newapp
```

**Pontos de atenção:**
- Liste os parâmetros do template **antes** de usá-lo.
- Compare os tipos de recurso criados por cada método (Secret, PVC...) e quais recebem labels.
- Lembre que `oc get all` não mostra todos os tipos.

---

## 4.4 Guided Exercise: Manage Long-lived and Short-lived Applications by Using the Kubernetes Workload API

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `deploy-workloads` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 251–255 |

**Competência praticada:** implantar um servidor de banco gerenciado por Deployment
e uma aplicação em lote gerenciada por Job; atualizar variáveis de ambiente no
template de Pod; criar e executar Jobs; ver logs e estado de término; inspecionar o
template de Pod do Job.

**Domine antes:** [4.3](4.3-workloads-de-longa-e-curta-duracao.md).

```bash
lab start deploy-workloads
lab finish deploy-workloads
```

**Pontos de atenção:**
- Variáveis obrigatórias de imagens de banco: sem elas, o Pod falha. Leia os logs.
- `oc set env` em um Deployment cria novos Pods; acompanhe o rollout.
- Para Jobs, confira a coluna de conclusões e o status do Pod (`Completed`).

---

## 4.6 Guided Exercise: Kubernetes Pod and Service Networks

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `deploy-services` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 265–270 |

**Competência praticada:** implantar um servidor de banco e acessá-lo indiretamente
por um Service e diretamente, Pod a Pod, para diagnóstico.

**Domine antes:** [4.5](4.5-redes-de-pods-e-services.md): seletor × labels,
EndpointSlices, DNS.

```bash
lab start deploy-services
lab finish deploy-services
```

**Pontos de atenção:**
- Avisos de segurança de Pod (PSA) podem ser ignorados no curso.
- Guardar nomes e IPs em variáveis de shell agiliza os testes.
- Confirme que o IP listado no EndpointSlice é o IP do Pod.

---

## 4.8 Guided Exercise: Scale and Expose Applications to External Access

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `deploy-routes` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 279–284 |

**Competência praticada:** implantar duas aplicações web; expor uma por Ingress e
outra por Route; habilitar sessões persistentes; escalar e verificar o
balanceamento entre os Pods.

**Domine antes:** [4.7](4.7-escalar-e-expor-aplicacoes.md).

```bash
lab start deploy-routes
lab finish deploy-routes
```

**Pontos de atenção:**
- Ingress e Route usam anotações **diferentes** para sessões persistentes.
- Use `curl` com e sem arquivo de cookies para ver a diferença.
- Após escalar, os endpoints do Service devem listar todas as réplicas.

---

## 4.9 Lab: Deploy Managed and Networked Applications on Kubernetes

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `deploy-review` |
| Avaliação | **`lab grade deploy-review`** |
| Referência | PDF p. 285–291 |

**Competência praticada (resumo autoral):** implantar um banco MySQL a partir de
imagem e descobrir a causa raiz de uma falha inicial; configurar variáveis de
ambiente de um Deployment; popular o banco; criar Services com nomes e portas
especificados; implantar uma aplicação web que usa o banco; expô-la por uma Route
e testar a ligação aplicação → banco pelo navegador.

**Domine antes:** as quatro lições e a [revisão](REVISAO.md).

```bash
lab start deploy-review
lab grade deploy-review
lab finish deploy-review
```

**Pontos de atenção:**
- O `lab grade` confere **nomes** de Deployments, Services e Route e as **portas**: siga o enunciado à risca.
- Comece pela causa da falha do banco: `oc get pods`, `oc logs`, `oc describe`.
- A aplicação web encontra o banco pelo **nome do Service**.
- Teste de fora pela Route e de dentro pelo Service, se algo não responder.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 4.7 Escalar e expor](4.7-escalar-e-expor-aplicacoes.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
