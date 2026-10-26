# Comandos `oc` por tarefa

> Cobertura atual: fundamentos e Capítulo 1. Ampliada a cada capítulo.
> Coluna **Perm.**: 👤 qualquer usuário autenticado · 🛡️ administrador do cluster.

## Sessão e contexto

| Comando | Para quê | Perm. | Lição |
|---------|----------|-------|-------|
| `oc login -u <usuario> <api>:6443` | Autenticar | — | [F8](../01-fundamentos-essenciais/08-ferramentas-de-administracao.md) |
| `oc whoami` | Usuário atual | 👤 | F8 |
| `oc whoami --show-console` | URL da web console | 👤 | [1.5](../capitulos/01-introducao-kubernetes-openshift/1.5-navegar-na-web-console.md) |
| `oc whoami --show-server` | URL da API | 👤 | F8 |
| `oc config get-contexts` | Contextos do kubeconfig | 👤 | F8 |
| `oc version` | Versões do cliente e do servidor | 👤 | F8 |

## Projetos

| Comando | Para quê | Perm. |
|---------|----------|-------|
| `oc get projects` | Projetos visíveis | 👤 |
| `oc project` | Projeto atual | 👤 |
| `oc project <nome>` | Mudar de projeto | 👤 |
| `oc new-project <nome> [--display-name=..] [--description=..]` | Criar projeto e entrar nele | 👤 (self-provisioner) |
| `oc delete project <nome>` | Apagar projeto **e tudo nele** | 👤 (dono) |

## Descobrir a API

| Comando | Para quê |
|---------|----------|
| `oc api-resources` | Tipos disponíveis, nomes curtos, escopo |
| `oc api-resources --namespaced=false` | Só tipos de escopo de cluster |
| `oc explain <tipo>[.campo...]` | Documentação de campos |
| `oc explain <tipo> --recursive` | Árvore completa de campos |

## Ler recursos

| Comando | Para quê |
|---------|----------|
| `oc get <tipo>` | Lista no projeto atual |
| `oc get <tipo> -A` | Lista em todos os namespaces (🛡️ para a maioria dos tipos) |
| `oc get <tipo> -o wide` | Colunas extras |
| `oc get <tipo> <nome> -o yaml` | Objeto completo (spec + status) |
| `oc get <tipo> -l chave=valor` | Filtrar por label |
| `oc get pods --show-labels` | Ver labels |
| `oc describe <tipo> <nome>` | Detalhe legível + eventos |

## Saúde da plataforma 🛡️

| Comando | Para quê | Lição |
|---------|----------|-------|
| `oc get clusterversion` | Versão e atualização em curso | [1.3](../capitulos/01-introducao-kubernetes-openshift/1.3-componentes-e-edicoes-do-openshift.md) |
| `oc get clusteroperators` | Available / Progressing / Degraded por componente | [F3](../01-fundamentos-essenciais/03-arquitetura-openshift.md) |
| `oc get nodes [-o wide]` | Nós, status, SO, runtime | [1.7](../capitulos/01-introducao-kubernetes-openshift/1.7-monitorar-um-cluster-openshift.md) |
| `oc describe node <nó>` | Capacidade, condições, eventos | F2 |
| `oc adm top nodes` | Consumo de CPU/memória | 1.7 |
| `oc debug node/<nó>` → `chroot /host` | Shell de diagnóstico no nó | 1.7 |
| `oc adm node-logs <nó> -u kubelet` | Logs de serviço do nó | 1.7 |
| `oc get machines -n openshift-machine-api` | Machines | 1.7 |
| `oc get machineconfig` / `oc get mcp` | MachineConfigs e pools | 1.7 |
| `oc get csv -A` | Operators instalados (OLM) | 1.5 |

## Aplicações (prévia; aprofundado nos capítulos 3–7)

| Comando | Para quê |
|---------|----------|
| `oc logs <pod> [-c <container>]` | Logs do container |
| `oc get events --sort-by=.lastTimestamp` | Eventos recentes |
| `oc apply -f <arquivo>` | Criar/atualizar declarativamente |
| `oc apply -f <arquivo> --dry-run=server` | Validar sem gravar |
| `oc diff -f <arquivo>` | O que mudaria |
| `oc scale deployment/<nome> --replicas=N` | Alterar réplicas |
| `oc expose service <nome>` | Criar Route |

---
[Início](../README.md) | [kubectl × oc →](kubectl-versus-oc.md)
