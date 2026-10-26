# Objetos Kubernetes e OpenShift

| Objeto | `apiVersion` | Escopo | Função em uma linha | Lição |
|--------|--------------|--------|---------------------|-------|
| Pod | `v1` | Namespace | 1+ containers no mesmo nó, mesmo IP; efêmero | [F4](../01-fundamentos-essenciais/04-pods-e-workloads.md) |
| ReplicaSet | `apps/v1` | Namespace | Mantém N Pods idênticos (gerenciado pelo Deployment) | F4 |
| Deployment | `apps/v1` | Namespace | Réplicas + rollout/rollback de apps stateless | F4 |
| StatefulSet | `apps/v1` | Namespace | Pods com identidade estável e volume próprio | F4, F7 |
| DaemonSet | `apps/v1` | Namespace | Um Pod por nó | F4 |
| Job | `batch/v1` | Namespace | Tarefa até a conclusão | F4 |
| CronJob | `batch/v1` | Namespace | Job agendado | F4 |
| Template | `template.openshift.io/v1` | Namespace | Definições parametrizadas de recursos (OpenShift) | [4.1](../capitulos/04-deploy-e-redes/4.1-implantar-a-partir-de-imagem-e-template.md) |
| Ingress | `networking.k8s.io/v1` | Namespace | Exposição HTTP(S) padrão Kubernetes | [4.7](../capitulos/04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md) |
| GatewayClass | `gateway.networking.k8s.io/v1` | Cluster | Controller de gateways | 4.7 |
| Gateway / HTTPRoute | `gateway.networking.k8s.io/v1` | Namespace | Ponto de entrada / regras HTTP | 4.7 |
| Network (config) | `config.openshift.io/v1` | Cluster | CIDRs e tipo de rede do cluster | [4.5](../capitulos/04-deploy-e-redes/4.5-redes-de-pods-e-services.md) |
| Service | `v1` | Namespace | IP virtual estável + DNS + balanceamento | [F6](../01-fundamentos-essenciais/06-redes-e-servicos.md) |
| EndpointSlice | `discovery.k8s.io/v1` | Namespace | IPs dos Pods prontos de um Service | F6 |
| Route | `route.openshift.io/v1` | Namespace | Hostname externo → Service (OpenShift) | F6 |
| ConfigMap | `v1` | Namespace | Configuração não sensível | Cap. 5 |
| Secret | `v1` | Namespace | Dado sensível (base64, **não** criptografado por padrão) | Cap. 5 |
| PersistentVolumeClaim | `v1` | Namespace | Pedido de storage | [F7](../01-fundamentos-essenciais/07-persistencia-de-dados.md) |
| PersistentVolume | `v1` | Cluster | Storage real | F7 |
| StorageClass | `storage.k8s.io/v1` | Cluster | Tipo de storage + provisionador | F7 |
| Namespace | `v1` | Cluster | Isolamento lógico e base de permissões | [F3](../01-fundamentos-essenciais/03-arquitetura-openshift.md) |
| Project | `project.openshift.io/v1` | Cluster | Visão OpenShift de um namespace | F3 |
| Node | `v1` | Cluster | Sistema que executa Pods | [1.7](../capitulos/01-introducao-kubernetes-openshift/1.7-monitorar-um-cluster-openshift.md) |
| Machine | `machine.openshift.io/v1beta1` | Namespace (`openshift-machine-api`) | Recurso que descreve/provisiona um nó | 1.7 |
| MachineConfig | `machineconfiguration.openshift.io/v1` | Cluster | Configuração declarada do SO dos nós | 1.7 |
| ClusterVersion | `config.openshift.io/v1` | Cluster | Versão e atualizações do cluster | [1.3](../capitulos/01-introducao-kubernetes-openshift/1.3-componentes-e-edicoes-do-openshift.md) |
| ClusterOperator | `config.openshift.io/v1` | Cluster | Estado de um componente da plataforma | F3 |
| ClusterServiceVersion | `operators.coreos.com/v1alpha1` | Namespace | Operator instalado via OLM | [1.5](../capitulos/01-introducao-kubernetes-openshift/1.5-navegar-na-web-console.md) |
| ServiceMonitor / PodMonitor | `monitoring.coreos.com/v1` | Namespace | Define coleta de métricas | 1.7 |
| Event | `v1` | Namespace | Registro de alto nível de algo que aconteceu | 1.7 |
| HorizontalPodAutoscaler | `autoscaling/v2` | Namespace | Ajusta réplicas por métricas | [6.9](../capitulos/06-confiabilidade/6.9-autoscaling-de-aplicacoes.md) |
| LimitRange | `v1` | Namespace | Requests/limits padrão e mínimos/máximos por projeto | 6.9 |

> Confirme `apiVersion` e escopo no seu cluster com `oc api-resources`.

---
[← kubectl × oc](kubectl-versus-oc.md) | [Início](../README.md) | [Exemplos YAML →](exemplos-yaml.md)
