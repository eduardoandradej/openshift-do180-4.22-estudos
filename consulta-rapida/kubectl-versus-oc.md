# `kubectl` × `oc`

## Regra geral

O `oc` **inclui** os comandos do `kubectl`, com a mesma sintaxe. Use `oc` no
OpenShift; a documentação de Kubernetes continua válida trocando `kubectl` por `oc`.

## Iguais nos dois

`get`, `describe`, `create`, `apply`, `delete`, `edit`, `patch`, `logs`, `exec`,
`explain`, `api-resources`, `scale`, `rollout`, `label`, `annotate`, `port-forward`,
`config`, `debug`.

## Só no `oc` (ou com comportamento próprio)

| Comando | Para quê | Por que não existe no `kubectl` |
|---------|----------|---------------------------------|
| `oc login` / `oc logout` | Autenticar via OAuth do cluster | Kubernetes não define login interativo |
| `oc whoami [--show-console]` | Identidade e URLs | Conceito de console é do OpenShift |
| `oc project` / `oc projects` / `oc new-project` | Trabalhar com Projects | Project é recurso OpenShift |
| `oc new-app` | Criar aplicação a partir de imagem, template ou código | Usa builds, ImageStreams, templates |
| `oc expose` (para Route) | Criar Route | Route é recurso OpenShift |
| `oc start-build`, `oc set triggers` | Builds e triggers de imagem | Recursos OpenShift |
| `oc adm ...` | Administração do cluster (`top`, `node-logs`, `must-gather`, `policy`) | Ferramentas da plataforma |

## Equivalências úteis

| Objetivo | `kubectl` | `oc` |
|----------|-----------|------|
| Mudar namespace atual | `kubectl config set-context --current --namespace=x` | `oc project x` |
| Criar namespace | `kubectl create namespace x` | `oc new-project x` (cria Project) |
| Consumo de nós | `kubectl top nodes` | `oc adm top nodes` |

---
[← Comandos oc](comandos-oc.md) | [Início](../README.md) | [Objetos Kubernetes →](objetos-kubernetes.md)
