# Glossário

| Termo | Definição |
|-------|-----------|
| **Alert** | Notificação gerada quando uma métrica deixa de atender a uma condição definida |
| **API Explorer** | Página da console que cataloga os tipos de recurso do cluster |
| **cgroups** | Recurso do kernel que limita consumo de CPU, memória etc. |
| **Cluster Observability Operator (COO)** | Componente opcional que adiciona pilhas de monitoramento customizáveis |
| **Cluster Operator** | Operator que gerencia um componente da plataforma OpenShift |
| **Control plane** | Conjunto de componentes que coordenam o cluster (API server, etcd, scheduler, controllers) |
| **Controller** | Laço que compara estado desejado e observado e age para igualá-los |
| **CRI-O** | Runtime de containers usado pelo kubelet nos nós do OpenShift |
| **Debug pod** | Pod temporário para diagnóstico de um nó (`oc debug node/...`) |
| **Declarativo** | Modelo em que se descreve o resultado, e não os passos |
| **Deployment** | Controller que mantém réplicas e gerencia versões de uma aplicação |
| **Digest** | Hash `sha256` que identifica de forma imutável o conteúdo de uma imagem |
| **Digital sovereignty** | Controle total da organização sobre infraestrutura, dados e fronteiras de segurança |
| **etcd** | Banco chave-valor que guarda o estado do cluster |
| **EUS** | Extended Update Support: suporte estendido das versões minor pares |
| **Event** | Registro de alto nível de algo relevante que aconteceu no cluster |
| **Hosted control plane** | Control plane executado como Pods em um cluster de hospedagem |
| **Image** | Pacote imutável em camadas a partir do qual containers são criados |
| **In-place pod resize** | Ajuste de CPU/memória de um Pod em execução sem reiniciá-lo (Kubernetes 1.35 / OCP 4.22) |
| **Insights Operator** | Envia dados do cluster para análise do Lightspeed advisor |
| **kubelet** | Agente que executa e monitora Pods em cada nó |
| **Label / Selector** | Par chave=valor em objetos / filtro que seleciona objetos por labels |
| **Lightspeed advisor** | Serviço no Hybrid Cloud Console que recomenda correções para o cluster |
| **Machine** | Recurso OpenShift que descreve um nó do cluster |
| **MachineConfig / MCO** | Configuração declarada do SO dos nós / operador que a aplica e mantém |
| **Namespace** | Divisão lógica de recursos e base de permissões |
| **Namespaces (kernel)** | Isolamento da visão de um processo (PID, rede, mount etc.) |
| **Node** | Máquina física ou virtual que executa Pods |
| **OCI** | Open Container Initiative: padrões de imagem e runtime |
| **Operator** | Controller que gerencia uma aplicação de forma declarativa |
| **Pod** | Menor unidade de execução: 1+ containers no mesmo nó |
| **Project** | Namespace com metadados adicionais no OpenShift |
| **PV / PVC** | Storage real (cluster) / pedido de storage (namespace) |
| **Registry** | Servidor que armazena e distribui imagens |
| **RHEL CoreOS** | SO imutável dos nós do OpenShift, gerenciado pelo cluster |
| **Route** | Exposição externa de um Service por hostname (OpenShift) |
| **S2I** | Source-to-Image: gera imagem a partir do código-fonte |
| **Service** | IP virtual estável e DNS que balanceia para Pods |
| **ServiceMonitor / PodMonitor** | Definem como coletar métricas de Services / Pods |
| **Software Catalog** | Catálogo unificado da console (4.19+) para Operators, Helm charts e outros softwares |
| **StorageClass** | Tipo de storage e seu provisionador dinâmico |
| **Tag** | Rótulo móvel de uma imagem (ex.: `latest`) |
| **UPI** | User Provisioned Infrastructure: instalação em infraestrutura preparada pelo usuário |

---
[← Troubleshooting](troubleshooting.md) | [Início](../README.md)
