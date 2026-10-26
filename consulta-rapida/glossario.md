# Glossário

| Termo | Definição |
|-------|-----------|
| **Alert** | Notificação gerada quando uma métrica deixa de atender a uma condição definida |
| **Allocatable** | Parte da capacidade de um nó disponível para Pods, após reservas do sistema |
| **API Explorer** | Página da console que cataloga os tipos de recurso do cluster |
| **cgroups** | Recurso do kernel que limita consumo de CPU, memória etc. |
| **Cluster Observability Operator (COO)** | Componente opcional que adiciona pilhas de monitoramento customizáveis |
| **Cluster Operator** | Operator que gerencia um componente da plataforma OpenShift |
| **Cluster Version Operator (CVO)** | Gerencia os cluster operators e as atualizações da plataforma |
| **ClusterImagePolicy** | Recurso que define verificação de assinatura (Sigstore) de imagens no cluster |
| **Condition** | Entrada do `status` (`type`, `status`, `reason`, `message`, `lastTransitionTime`) que explica o estado de um objeto |
| **Control plane** | Conjunto de componentes que coordenam o cluster (API server, etcd, scheduler, controllers) |
| **Controller** | Laço que compara estado desejado e observado e age para igualá-los |
| **CRI** | Container Runtime Interface: padrão de integração entre o kubelet e o runtime |
| **CRI-O** | Runtime de containers usado pelo kubelet nos nós do OpenShift |
| **crictl** | CLI do CRI-O usada nos nós para inspecionar Pods, containers e imagens |
| **Debug pod** | Pod temporário para diagnóstico de um nó (`oc debug node/...`) |
| **Declarativo** | Modelo em que se descreve o resultado, e não os passos |
| **Deployment** | Controller que mantém réplicas e gerencia versões de uma aplicação |
| **Digest** | Hash `sha256` que identifica de forma imutável o conteúdo de uma imagem |
| **Digital sovereignty** | Controle total da organização sobre infraestrutura, dados e fronteiras de segurança |
| **etcd** | Banco chave-valor que guarda o estado do cluster |
| **EUS** | Extended Update Support: suporte estendido das versões minor pares |
| **Event** | Registro de alto nível de algo relevante que aconteceu no cluster |
| **Floating tag** | Tag que é apelido de outra e muda a cada novo build (ex.: `latest`) |
| **Hosted control plane** | Control plane executado como Pods em um cluster de hospedagem |
| **Image** | Pacote imutável em camadas a partir do qual containers são criados |
| **In-place pod resize** | Ajuste de CPU/memória de um Pod em execução sem reiniciá-lo (Kubernetes 1.35 / OCP 4.22) |
| **Insights Operator** | Envia dados do cluster para análise do Lightspeed advisor |
| **JSONPath** | Linguagem de consulta a JSON embutida no `oc`/`kubectl` (`-o jsonpath`) |
| **kubelet** | Agente que executa e monitora Pods em cada nó |
| **Label / Selector** | Par chave=valor em objetos / filtro que seleciona objetos por labels |
| **Lightspeed advisor** | Serviço no Hybrid Cloud Console que recomenda correções para o cluster |
| **Machine** | Recurso OpenShift que descreve um nó do cluster |
| **MachineConfig / MCO** | Configuração declarada do SO dos nós / operador que a aplica e mantém |
| **must-gather** | `oc adm must-gather`: coleta definições e logs do cluster para o suporte |
| **Namespace** | Divisão lógica de recursos e base de permissões |
| **Namespaces (kernel)** | Isolamento da visão de um processo (PID, rede, mount etc.) |
| **Node** | Máquina física ou virtual que executa Pods |
| **nsenter** | Ferramenta que executa comandos dentro dos namespaces de um processo |
| **OAuth server** | Servidor embutido no control plane que emite tokens de acesso |
| **OCI** | Open Container Initiative: padrões de imagem e runtime |
| **OLM** | Operator Lifecycle Manager: gerencia operators adicionais |
| **Operator** | Controller que gerencia uma aplicação de forma declarativa |
| **Pod** | Menor unidade de execução: 1+ containers no mesmo nó |
| **Port forwarding** | Túnel temporário de uma porta local até a porta de um Pod (`oc port-forward`) |
| **Project** | Namespace com metadados adicionais no OpenShift |
| **PSA** | Pod Security Admission: perfis `privileged`, `baseline`, `restricted` por namespace |
| **PV / PVC** | Storage real (cluster) / pedido de storage (namespace) |
| **Registry** | Servidor que armazena e distribui imagens |
| **restartPolicy** | Política de reinício de containers de um Pod: `Always`, `OnFailure`, `Never` |
| **RHEL CoreOS** | SO imutável dos nós do OpenShift, gerenciado pelo cluster |
| **Route** | Exposição externa de um Service por hostname (OpenShift) |
| **S2I** | Source-to-Image: gera imagem a partir do código-fonte |
| **SCC** | Security Context Constraints: controlam permissões de segurança de Pods no OpenShift |
| **Service** | IP virtual estável e DNS que balanceia para Pods |
| **ServiceAccount** | Conta usada por aplicações para acessar a API |
| **ServiceMonitor / PodMonitor** | Definem como coletar métricas de Services / Pods |
| **Sigstore** | Projeto para assinar e verificar imagens de container |
| **Skopeo** | Ferramenta para inspecionar, copiar e sincronizar imagens remotas sem daemon |
| **Software Catalog** | Catálogo unificado da console (4.19+) para Operators, Helm charts e outros softwares |
| **StorageClass** | Tipo de storage e seu provisionador dinâmico |
| **Tag** | Rótulo móvel de uma imagem (ex.: `latest`) |
| **UBI** | Universal Base Image: imagens base Red Hat redistribuíveis (standard, init, minimal, micro) |
| **uid-range** | Anotação do projeto com a faixa de UIDs atribuída aos containers |
| **UPI** | User Provisioned Infrastructure: instalação em infraestrutura preparada pelo usuário |

---
[← Troubleshooting](troubleshooting.md) | [Início](../README.md)
