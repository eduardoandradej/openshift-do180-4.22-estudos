# Comandos `oc` por tarefa

> Cobertura atual: fundamentos e Capítulos 1–7. Ampliada a cada capítulo.
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
| `oc login --token=<t> --server=<api>` | Login por token (recomendado) | — | [2.1](../capitulos/02-cli-e-apis/2.1-interfaces-de-linha-de-comando.md) |
| `oc login --web <api>` | Login pelo navegador (SSO) | — | 2.1 |
| `oc cluster-info` | Endereço do control plane | 👤 | 2.1 |
| `oc api-versions` | Pares `grupo/versão` suportados | 👤 | 2.1 |
| `oc config use-context <ctx>` | Alternar contexto | 👤 | 2.1 |

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
| `oc api-resources --api-group ''` | Tipos do grupo core |
| `oc api-resources --api-group apps --sort-by name` | Tipos de um grupo, ordenados |
| `oc api-resources --namespaced -o name \| wc -l` | Contar tipos de namespace |

## Ler recursos

| Comando | Para quê |
|---------|----------|
| `oc get <tipo>` | Lista no projeto atual |
| `oc get <tipo> -A` | Lista em todos os namespaces (🛡️ para a maioria dos tipos) |
| `oc get <tipo> -o wide` | Colunas extras |
| `oc get <tipo> <nome> -o yaml` | Objeto completo (spec + status) |
| `oc get <tipo> -l chave=valor` | Filtrar por label |
| `oc get pods --show-labels` | Ver labels |
| `oc describe <tipo> <nome>` | Detalhe legível + eventos (não use em scripts) |
| `oc get all` | Tipos principais do projeto (não inclui ConfigMaps, Secrets, PVCs) |
| `oc status --suggest` | Visão geral do projeto com dicas |

## Formatar e filtrar saídas ([2.3](../capitulos/02-cli-e-apis/2.3-inspecionar-recursos-kubernetes.md))

| Comando | Para quê |
|---------|----------|
| `oc get pod <p> -o jsonpath='{.status.podIP}{"\n"}'` | Um campo de um objeto |
| `oc get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}'` | Laço sobre uma lista |
| `oc get node <n> -o jsonpath='{.status.addresses[?(@.type=="InternalIP")].address}'` | Filtro dentro de uma lista |
| `oc get pods -o custom-columns=POD:.metadata.name,IP:.status.podIP` | Tabela personalizada |
| `oc get pods -o json \| jq '.items[].status.podIP'` | Consulta com `jq` |
| `oc get pods -o yaml \| yq '.items[0].status.podIP'` | Consulta com `yq` (Mike Farah) |
| `oc get pods -o go-template='{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'` | Go template |

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
| `oc get operators` | Operators adicionais do OLM | [2.5](../capitulos/02-cli-e-apis/2.5-avaliar-a-saude-do-cluster.md) |
| `oc get co <x> -o jsonpath='{.status.conditions}' \| jq` | Conditions de um cluster operator | 2.5 |
| `oc adm top pods -A --sum` | Consumo de todos os Pods + total | 2.5 |
| `oc adm top pods <p> -n <ns> --containers` | Consumo por container | 2.5 |
| `oc adm node-logs <nó> -u crio --tail N` | Últimas linhas de uma unidade | 2.5 |
| `oc adm node-logs --role master -u kubelet` | Logs por papel de nó | 2.5 |
| `oc get node <n> -o jsonpath='{.status.allocatable}'` | Recursos alocáveis | 2.5 |
| `oc adm must-gather --dest-dir <dir>` | Coleta para suporte | 2.5 |
| `oc adm inspect clusteroperator/<x> --since 10m --dest-dir <dir>` | Coleta de um componente | 2.5 |

## Pods e containers ([3.1](../capitulos/03-containers-e-pods/3.1-criar-containers-e-pods.md), [3.5](../capitulos/03-containers-e-pods/3.5-diagnosticar-containers-e-pods.md))

| Comando | Para quê |
|---------|----------|
| `oc run <n> --image <img> [--env K=V]` | Criar Pod avulso |
| `oc run <n> -it --rm --restart Never --image <img> --command -- <cmd>` | Comando pontual, Pod apagado ao final |
| `oc describe project <p> \| grep scc` | Faixas de UID/GID do projeto |
| `oc exec <pod> [-c <c>] -- <cmd>` | Comando no container |
| `oc exec -it <pod> -- bash -il` | Shell interativo |
| `oc rsh [-c <c>] <pod>` | Shell remoto |
| `oc attach <pod> -it` | Conectar ao processo principal |
| `oc logs <pod> [-f] [-p] [--tail N] [-c <c>]` | Logs (atual ou instância anterior) |
| `oc delete pod <n> [--grace-period N\|--now\|--force]` | Apagar Pod |
| `oc delete pod -l <label>` / `oc delete pods --all` | Apagar por label / todos |
| `oc edit pod <n>` | Editar no editor (`KUBE_EDITOR`) |
| `oc patch pod <n> --type=json -p '[{"op":"replace","path":"/spec/containers/0/image","value":"<img>"}]'` | Trocar imagem |
| `oc cp <orig> <pod>:<dest> [-c <c>]` | Copiar arquivos (precisa de `tar`) |
| `oc rsync <pod>:<dir> <local>` | Sincronizar diretórios |
| `oc port-forward pod/<n> <local>:<remota>` | Túnel temporário até o Pod |

## No nó, como administrador ([3.1](../capitulos/03-containers-e-pods/3.1-criar-containers-e-pods.md))

| Comando | Para quê |
|---------|----------|
| `crictl ps --name <c>` | Container em execução |
| `crictl inspect -o json <id> \| jq .info.pid` | PID do container |
| `crictl pods` / `crictl images` / `crictl logs <id>` | Pods, imagens, logs no nó |
| `lsns -p <PID>` | Namespaces do processo |
| `nsenter -t <PID> -p -r <cmd>` / `-a` | Entrar no namespace PID / em todos |

## Imagens ([3.3](../capitulos/03-containers-e-pods/3.3-encontrar-e-inspecionar-imagens.md))

| Comando | Para quê |
|---------|----------|
| `skopeo login <registry>` | Autenticar no registry |
| `skopeo list-tags docker://<repo>` | Tags disponíveis |
| `skopeo inspect [--config] docker://<img>` | Digest, tags, User, Env, Entrypoint, Cmd |
| `skopeo copy docker://<a> docker://<b>` | Copiar imagem |
| `skopeo sync --src docker --dest docker <a> <b>` | Sincronizar repositório |
| `oc image info <img> [--filter-by-os amd64]` | Informações da imagem |
| `oc image extract <img> --path <orig>:<dest>` | Extrair arquivos sem rodar |
| `oc image mirror <a> <b>` | Espelhar entre registries |

## Implantar aplicações ([4.1](../capitulos/04-deploy-e-redes/4.1-implantar-a-partir-de-imagem-e-template.md), [4.3](../capitulos/04-deploy-e-redes/4.3-workloads-de-longa-e-curta-duracao.md))

| Comando | Para quê |
|---------|----------|
| `oc get templates -n openshift` | Templates predefinidos |
| `oc process --parameters <t> -n openshift` | Parâmetros de um template |
| `oc process -f <arq> -p K=V \| oc apply -f -` | Processar e aplicar template |
| `oc new-app --template <t> --param K=V` | Criar a partir de template |
| `oc new-app --image <img> [--name <n>]` | Criar a partir de imagem |
| `oc new-app <url-git>#<ref> --name <n>` | Criar a partir de Git |
| `oc create deployment <n> --image <img> [--replicas N]` | Criar Deployment |
| `oc create deployment <n> --image <img> --dry-run=client -o yaml` | Gerar manifesto |
| `oc set env deployment/<n> K=V` | Variáveis no template de Pod |
| `oc create job <n> --image <img> -- <cmd>` | Job |
| `oc create cronjob <n> --image <img> --schedule "<cron>" -- <cmd>` | CronJob |
| `oc create job <n> --from=cronjob/<cj>` | Disparar CronJob manualmente |
| `oc api-resources --categories=all` | Tipos incluídos em `all` |

## Rede e exposição ([4.5](../capitulos/04-deploy-e-redes/4.5-redes-de-pods-e-services.md), [4.7](../capitulos/04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md))

| Comando | Para quê |
|---------|----------|
| `oc expose deployment/<d> [--port P] [--target-port T] [--name N]` | Criar Service |
| `oc expose deployment/<d> --type NodePort --port P` | Service NodePort |
| `oc create service externalname <n> --external-name <fqdn>` | Service ExternalName |
| `oc get svc -o wide` | Services com seletor |
| `oc get endpointslices -l kubernetes.io/service-name=<svc>` | Endpoints de um Service |
| `oc describe network.config/cluster` | CIDRs de Pods e Services (admin) |
| `oc expose service <svc> [--hostname H] [--name N]` | Criar Route |
| `oc get route <r> -o jsonpath='{.spec.host}'` | Hostname da Route |
| `oc create ingress <n> --rule="host/*=svc:porta"` | Criar Ingress |
| `oc annotate route <r> router.openshift.io/cookie_name=<c>` | Sticky session em Route |
| `oc annotate ingress <i> ingress.kubernetes.io/affinity=cookie` | Sticky session em Ingress |
| `oc scale --replicas=N deployment/<d>` | Escalar |

## Configuração ([5.1](../capitulos/05-configuracao-e-storage/5.1-externalizar-configuracao.md))

| Comando | Para quê |
|---------|----------|
| `oc create secret generic <s> --from-literal k=v` / `--from-file k=arq` | Secret Opaque |
| `oc create secret tls <s> --cert <crt> --key <key>` | Secret TLS |
| `oc create cm <c> --from-literal k=v` / `--from-file arq` | ConfigMap |
| `oc set env deployment/<d> --from configmap/<c>` | Todas as chaves como variáveis |
| `oc set env deployment/<d> --from secret/<s> --prefix P_` | Variáveis com prefixo (chaves em maiúsculas) |
| `oc set env deployment/<d> --list` | Ver variáveis |
| `oc set volume deployment/<d> --add --type configmap --configmap-name <c> --mount-path <p>` | ConfigMap como arquivos |
| `oc set volume deployment/<d> --add --type secret --secret-name <s> --mount-path <p>` | Secret como arquivos |
| `oc extract secret/<s> --to <dir> --confirm` | Baixar chaves para arquivos |
| `oc set data secret/<s> --from-file <arq>` / `oc set data cm/<c> k=v` | Atualizar dados |
| `oc rollout restart deployment/<d>` | Reiniciar Pods para ler variáveis novas |

## Storage ([5.3](../capitulos/05-configuracao-e-storage/5.3-provisionar-volumes-persistentes.md), [5.5](../capitulos/05-configuracao-e-storage/5.5-selecionar-storage-class.md), [5.7](../capitulos/05-configuracao-e-storage/5.7-storage-nao-compartilhado-com-statefulsets.md))

| Comando | Para quê |
|---------|----------|
| `oc set volumes deployment/<d> --add --type pvc --claim-name <c> --claim-size <t> --claim-mode rwo --claim-class <sc> --mount-path <p>` | Criar e montar PVC |
| `oc set volumes deployment/<d> --add --name <v> --claim-name <c> --mount-path <p>` | Montar PVC existente |
| `oc set volume deployment/<d>` / `--remove --name <v>` | Listar / remover volumes |
| `oc get pvc` / `oc describe pvc <c>` | Estado e eventos do PVC |
| `oc get pv` | PVs (admin) |
| `oc get storageclass` / `oc describe sc <x>` | Classes e parâmetros |
| `oc patch pvc/<c> --type merge -p '{"spec":{"resources":{"requests":{"storage":"<t>"}}}}'` | Expandir PVC |
| `oc get statefulset` / `oc scale statefulset/<s> --replicas N` | StatefulSets |

## Confiabilidade ([6.3](../capitulos/06-confiabilidade/6.3-health-probes.md), [6.5](../capitulos/06-confiabilidade/6.5-reservar-capacidade-de-computacao.md), [6.7](../capitulos/06-confiabilidade/6.7-limitar-capacidade-de-computacao.md), [6.9](../capitulos/06-confiabilidade/6.9-autoscaling-de-aplicacoes.md))

| Comando | Para quê |
|---------|----------|
| `oc set probe deployment/<d> --readiness --get-url http://:<p>/<caminho>` | Readiness HTTP |
| `oc set probe deployment/<d> --liveness --open-tcp <p>` | Liveness TCP |
| `oc set probe deployment/<d> --startup --get-url ... --period-seconds 10 --failure-threshold 30` | Startup para inicialização lenta |
| `oc set probe deployment/<d> --liveness -- <cmd>` | Probe por comando |
| `oc set probe deployment/<d> --liveness --remove` | Remover probe |
| `oc set resources deployment/<d> --requests cpu=100m,memory=256Mi` | Requests |
| `oc set resources deployment/<d> --limits cpu=500m,memory=512Mi` | Limits |
| `oc describe node <n>` | Capacity, Allocatable, requests e limits alocados |
| `oc get events --field-selector reason=FailedScheduling` | Pods que não couberam |
| `oc patch pod <p> --subresource resize --type merge -p '{"spec":{"containers":[...]}}'` | Redimensionar no local (4.22) |
| `oc autoscale deployment/<d> --min N --max M --cpu P%` | Criar HPA |
| `oc get hpa` / `oc describe hpa <h>` | Estado e eventos do HPA |
| `oc explain hpa.spec.metrics.resource.target` | Campos do alvo do HPA |

## Atualizações ([7.1](../capitulos/07-atualizacao-aplicacoes/7.1-identidade-e-tags-de-imagens.md), [7.3](../capitulos/07-atualizacao-aplicacoes/7.3-atualizar-imagem-e-configuracoes.md), [7.5](../capitulos/07-atualizacao-aplicacoes/7.5-implantacoes-reproduziveis-com-imagestreams.md), [7.7](../capitulos/07-atualizacao-aplicacoes/7.7-triggers-de-mudanca-de-imagem.md))

| Comando | Para quê |
|---------|----------|
| `oc image info --filter-by-os linux/amd64 <img>` | Digest de uma tag (imagem multiarquitetura) |
| `oc get pod <p> -o jsonpath='{.status.containerStatuses[*].imageID}'` | Digest em execução |
| `oc set image deployment/<d> <container>=<img>` | Trocar imagem |
| `oc rollout pause\|resume deployment/<d>` | Agrupar mudanças em um rollout |
| `oc rollout status deployment/<d>` | Acompanhar rollout |
| `oc rollout history deployment/<d> [--revision N]` | Revisões |
| `oc rollout undo deployment/<d> [--to-revision N]` | Rollback |
| `oc annotate deployment/<d> kubernetes.io/change-cause="..." --overwrite` | Descrever a revisão |
| `oc import-image <is:tag> --from <img> --confirm` | Criar/atualizar ImageStreamTag |
| `oc tag <img> <is:tag> [--scheduled] [--reference-policy local]` | Apontar tag; verificação periódica; pull-through |
| `oc create istag <is:tag> --from-image <img>` | Criar istag (só criação) |
| `oc tag --alias <is:origem> <is:alias>` | Alias de istag |
| `oc set image-lookup <is>` / `oc set image-lookup` | Lookup local / listar |
| `oc describe is <is>` / `oc get istag` | Digest atual (`*`) e histórico |
| `oc set triggers deployment/<d> --from-image <is:tag> --containers <c>` | Image trigger |
| `oc set triggers deployment/<d> [--auto\|--manual\|--remove-all]` | Ver/ligar/desligar triggers |

## Aplicações (prévia)

| Comando | Para quê |
|---------|----------|
| `oc logs <pod> [-c <container>]` | Logs do container |
| `oc get events --sort-by=.lastTimestamp` | Eventos recentes |
| `oc get events -A --sort-by .metadata.creationTimestamp` | Eventos de todo o cluster, em ordem |
| `oc debug deployment/<x> [--as-user=UID\|--as-root]` | Cópia de depuração do Pod |
| `oc debug --image=<imagem>` | Shell em uma imagem específica |
| `oc apply -f <arquivo>` | Criar/atualizar declarativamente |
| `oc apply -f <arquivo> --dry-run=server` | Validar sem gravar |
| `oc diff -f <arquivo>` | O que mudaria |
| `oc scale deployment/<nome> --replicas=N` | Alterar réplicas |
| `oc expose service <nome>` | Criar Route |

---
[Início](../README.md) | [kubectl × oc →](kubectl-versus-oc.md)
