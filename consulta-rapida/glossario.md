# Glossário

| Termo | Definição |
|-------|-----------|
| **Alert** | Notificação gerada quando uma métrica deixa de atender a uma condição definida |
| **Allocatable** | Parte da capacidade de um nó disponível para Pods, após reservas do sistema |
| **API Explorer** | Página da console que cataloga os tipos de recurso do cluster |
| **binaryData** | Campo do ConfigMap para conteúdo binário em base64 |
| **cgroups** | Recurso do kernel que limita consumo de CPU, memória etc. |
| **Cluster Observability Operator (COO)** | Componente opcional que adiciona pilhas de monitoramento customizáveis |
| **Cluster Operator** | Operator que gerencia um componente da plataforma OpenShift |
| **Cluster Version Operator (CVO)** | Gerencia os cluster operators e as atualizações da plataforma |
| **ClusterImagePolicy** | Recurso que define verificação de assinatura (Sigstore) de imagens no cluster |
| **CNI** | Container Network Interface: padrão de plugins de rede (ex.: OVN-Kubernetes) |
| **CNO** | Cluster Network Operator: configura a rede e os plugins CNI do OpenShift |
| **Condition** | Entrada do `status` (`type`, `status`, `reason`, `message`, `lastTransitionTime`) que explica o estado de um objeto |
| **ConfigMap** | Objeto com configuração não sensível consumida como variáveis ou arquivos |
| **Control plane** | Conjunto de componentes que coordenam o cluster (API server, etcd, scheduler, controllers) |
| **Controller** | Laço que compara estado desejado e observado e age para igualá-los |
| **CoreDNS** | Servidor DNS interno do cluster, implantado pelo DNS operator |
| **CRI** | Container Runtime Interface: padrão de integração entre o kubelet e o runtime |
| **CRI-O** | Runtime de containers usado pelo kubelet nos nós do OpenShift |
| **crictl** | CLI do CRI-O usada nos nós para inspecionar Pods, containers e imagens |
| **CronJob** | Cria Jobs periodicamente conforme agenda no formato cron |
| **DaemonSet** | Garante um Pod em todos (ou alguns) nós |
| **Debug pod** | Pod temporário para diagnóstico de um nó (`oc debug node/...`) |
| **Declarativo** | Modelo em que se descreve o resultado, e não os passos |
| **Deployment** | Controller que mantém réplicas e gerencia versões de uma aplicação |
| **DeploymentConfig** | Objeto antigo do OpenShift para implantações; obsoleto desde 4.14 |
| **Digest** | Hash `sha256` que identifica de forma imutável o conteúdo de uma imagem |
| **Digital sovereignty** | Controle total da organização sobre infraestrutura, dados e fronteiras de segurança |
| **etcd** | Banco chave-valor que guarda o estado do cluster |
| **EUS** | Extended Update Support: suporte estendido das versões minor pares |
| **Event** | Registro de alto nível de algo relevante que aconteceu no cluster |
| **ExternalName** | Tipo de Service que responde um CNAME para um nome externo |
| **FailedScheduling** | Evento de Pod que nenhum nó pôde receber |
| **Floating tag** | Tag que é apelido de outra e muda a cada novo build (ex.: `latest`) |
| **Gateway API** | Framework de entrada de tráfego com GatewayClass, Gateway e HTTPRoute |
| **Headless Service** | Service com `clusterIP: None`; o DNS devolve os IPs dos Pods |
| **Hosted control plane** | Control plane executado como Pods em um cluster de hospedagem |
| **hostPath** | Volume que monta um caminho do nó; exige Pod privilegiado |
| **HPA** | Horizontal Pod Autoscaler: ajusta o número de réplicas por métricas |
| **Image** | Pacote imutável em camadas a partir do qual containers são criados |
| **In-place pod resize** | Ajuste de CPU/memória de um Pod em execução sem reiniciá-lo (Kubernetes 1.35 / OCP 4.22) |
| **Ingress** | Recurso Kubernetes de exposição HTTP(S); no OpenShift gera uma Route gerenciada |
| **Insights Operator** | Envia dados do cluster para análise do Lightspeed advisor |
| **Job** | Executa uma tarefa em Pods até concluir, com novas tentativas em caso de falha |
| **JSONPath** | Linguagem de consulta a JSON embutida no `oc`/`kubectl` (`-o jsonpath`) |
| **kubelet** | Agente que executa e monitora Pods em cada nó |
| **Label / Selector** | Par chave=valor em objetos / filtro que seleciona objetos por labels |
| **Lightspeed advisor** | Serviço no Hybrid Cloud Console que recomenda correções para o cluster |
| **Limit** | Teto de CPU/memória de um container |
| **Liveness probe** | Teste que reinicia o container quando falha |
| **Machine** | Recurso OpenShift que descreve um nó do cluster |
| **MachineConfig / MCO** | Configuração declarada do SO dos nós / operador que a aplica e mantém |
| **Millicore** | Milésimo de um núcleo de CPU (`1000m` = 1 CPU) |
| **must-gather** | `oc adm must-gather`: coleta definições e logs do cluster para o suporte |
| **Namespace** | Divisão lógica de recursos e base de permissões |
| **Namespaces (kernel)** | Isolamento da visão de um processo (PID, rede, mount etc.) |
| **Node** | Máquina física ou virtual que executa Pods |
| **NodePort** | Tipo de Service que abre uma porta (30000–32767) em todos os nós |
| **nsenter** | Ferramenta que executa comandos dentro dos namespaces de um processo |
| **OAuth server** | Servidor embutido no control plane que emite tokens de acesso |
| **OCI** | Open Container Initiative: padrões de imagem e runtime |
| **OLM** | Operator Lifecycle Manager: gerencia operators adicionais |
| **OOMKilled** | Container encerrado pelo OOM killer ao atingir o limit de memória (exit 137) |
| **Operator** | Controller que gerencia uma aplicação de forma declarativa |
| **Overcommit** | Soma dos limits acima da capacidade do nó |
| **OVN-Kubernetes** | Plugin CNI padrão do OpenShift, baseado em Open Virtual Network |
| **Pod** | Menor unidade de execução: 1+ containers no mesmo nó |
| **Port forwarding** | Túnel temporário de uma porta local até a porta de um Pod (`oc port-forward`) |
| **Project** | Namespace com metadados adicionais no OpenShift |
| **PSA** | Pod Security Admission: perfis `privileged`, `baseline`, `restricted` por namespace |
| **PV / PVC** | Storage real (cluster) / pedido de storage (namespace) |
| **QoS class** | Guaranteed, Burstable ou BestEffort, conforme requests e limits |
| **Readiness probe** | Teste que decide se o Pod recebe tráfego |
| **Reclaim policy** | O que acontece com o PV após o PVC ser apagado: `Retain` ou `Delete` |
| **Registry** | Servidor que armazena e distribui imagens |
| **Request** | Reserva mínima de CPU/memória usada no agendamento |
| **restartPolicy** | Política de reinício de containers de um Pod: `Always`, `OnFailure`, `Never` |
| **RHEL CoreOS** | SO imutável dos nós do OpenShift, gerenciado pelo cluster |
| **Route** | Exposição externa de um Service por hostname (OpenShift) |
| **RWOP** | ReadWriteOncePod: leitura e escrita por um único Pod |
| **S2I** | Source-to-Image: gera imagem a partir do código-fonte |
| **SCC** | Security Context Constraints: controlam permissões de segurança de Pods no OpenShift |
| **Secret** | Objeto para dados sensíveis; valores em base64 (não criptografados) |
| **Service** | IP virtual estável e DNS que balanceia para Pods |
| **ServiceAccount** | Conta usada por aplicações para acessar a API |
| **ServiceMonitor / PodMonitor** | Definem como coletar métricas de Services / Pods |
| **Sigstore** | Projeto para assinar e verificar imagens de container |
| **Skopeo** | Ferramenta para inspecionar, copiar e sincronizar imagens remotas sem daemon |
| **Software Catalog** | Catálogo unificado da console (4.19+) para Operators, Helm charts e outros softwares |
| **Startup probe** | Teste que protege a inicialização; para após o primeiro sucesso |
| **StatefulSet** | Workload com Pods de identidade estável e um PVC por réplica |
| **Sticky session** | Afinidade de sessão por cookie no Ingress Controller |
| **Storage Object in Use Protection** | Adia a remoção de PVC/PV em uso para evitar perda de dados |
| **StorageClass** | Tipo de storage e seu provisionador dinâmico |
| **Tag** | Rótulo móvel de uma imagem (ex.: `latest`) |
| **Template** | Recurso OpenShift com definições parametrizadas de vários recursos |
| **Throttling** | Redução de velocidade de um container que atingiu o limit de CPU |
| **UBI** | Universal Base Image: imagens base Red Hat redistribuíveis (standard, init, minimal, micro) |
| **uid-range** | Anotação do projeto com a faixa de UIDs atribuída aos containers |
| **UPI** | User Provisioned Infrastructure: instalação em infraestrutura preparada pelo usuário |
| **volumeBindingMode** | Quando o PV é criado: `Immediate` ou `WaitForFirstConsumer` |
| **volumeClaimTemplates** | Modelo de PVC de um StatefulSet, um por réplica |
| **volumeMode** | `Filesystem` (padrão) ou `Block` (dispositivo cru) |
| **VPA** | Vertical Pod Autoscaler: ajusta requests e limits de cada Pod |

---
[← Troubleshooting](troubleshooting.md) | [Início](../README.md)
