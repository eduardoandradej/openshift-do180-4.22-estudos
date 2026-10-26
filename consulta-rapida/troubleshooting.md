# Troubleshooting: sintoma → causa → verificação

> Cobertura atual: fundamentos e Capítulos 1–7.

## Acesso e CLI

| Sintoma | Causa provável | Como verificar / resolver |
|---------|----------------|---------------------------|
| `Unauthorized` | Token expirado | `oc login` novamente |
| `Forbidden` | Usuário sem permissão | `oc whoami`; usar conta adequada |
| `NotFound` para recurso que existe | Projeto errado | `oc project`; usar `-n <ns>` |
| `x509: certificate signed by unknown authority` | CA do cluster não confiável | Instalar a CA ou, só em teste, `--insecure-skip-tls-verify` |
| Console sem menus de administração | Usuário não é admin | Conferir usuário logado |

## Cluster e nós

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| Nó `NotReady` | kubelet parado, rede, pressão de recursos | `oc describe node`; `oc debug node/<nó>` → `chroot /host` → `systemctl status kubelet crio` |
| Cluster Operator `Degraded True` | Componente fora do estado desejado | `oc describe co <nome>`; eventos no namespace do operador |
| MachineConfigPool `UPDATING True` por muito tempo | MCO aplicando ou travado em um nó | `oc get mcp`; `oc get nodes` |
| Alerta disparando | Condição de regra atingida | Observe › Alerting › regra (descrição e expressão); ou API do Alertmanager via `oc exec` |
| Condition `MemoryPressure` / `DiskPressure` / `PIDPressure` = `True` | Nó sem memória / disco / PIDs | `oc get node <n> -o json \| jq .status.conditions`; `oc adm top nodes`; com `DiskPressure`, Pods podem ser despejados |
| `NetworkUnavailable` = `True` | Rede do nó mal configurada | `oc describe node`; Cluster Operator `network` |
| `SchedulingDisabled` no STATUS | Nó isolado (*cordon*) | Normal durante manutenção; caso contrário, investigar quem isolou |
| `oc adm top`: `metrics not available yet` | Pod recém-criado ou monitoramento degradado | Aguardar; `oc get co monitoring` |
| Script com `oc describe` quebrou após atualização | Formato do `describe` mudou | Usar `-o json`/`jsonpath`/`custom-columns` |
| `oc logs` pede um container | Pod com vários containers | `-c <container>` |

## Pods e imagens ([3.5](../capitulos/03-containers-e-pods/3.5-diagnosticar-containers-e-pods.md))

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| `ErrImagePull` / `ImagePullBackOff` com `manifest unknown` | Tag ou repositório inexistente | `skopeo list-tags docker://<repo>` |
| `ImagePullBackOff` com `unauthorized` | Registry exige credencial | `oc describe pod`; credenciais do registry |
| `CrashLoopBackOff` com comando curto | `restartPolicy: Always` reinicia um processo que terminou com sucesso | Usar `--restart Never` ou um Job |
| `CrashLoopBackOff` com `Permission denied` | Imagem espera root; OpenShift roda com UID aleatório e GID 0 | `oc logs --previous`; `skopeo inspect --config` (`User`); `oc debug` + `ls -ld` |
| Falha ao escutar na porta 80/443 | Usuário não root não usa portas < 1024 | Usar imagem que escuta em 8080/8443 |
| `CreateContainerConfigError` | ConfigMap/Secret referenciado não existe | `oc describe pod` |
| `oc edit pod` recusa a alteração | Campo imutável do Pod (só a imagem muda) | Recriar o Pod ou usar Deployment |
| `oc cp` falha com erro de `tar` | Imagem sem `tar` | `oc rsync`, `oc exec -i ... cat >`, ou incluir na imagem |
| `port-forward`: `address already in use` | Porta local ocupada | Outra porta local (`18080:8080`) |
| `skopeo`: `Invalid image name` | Faltou o transporte | Prefixo `docker://` |

## Deploy, rede e exposição ([4.5](../capitulos/04-deploy-e-redes/4.5-redes-de-pods-e-services.md), [4.7](../capitulos/04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md))

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| Service sem endpoints | Seletor ≠ labels; Pods não prontos | `oc get svc -o wide`; `oc get pods --show-labels`; `oc get endpointslices -l kubernetes.io/service-name=<svc>` |
| Conecta pelo IP do Pod, não pelo Service | `port`/`targetPort` errados ou seletor | `oc describe svc` |
| Nome do Service não resolve | Service em outro projeto | Usar `svc.projeto` |
| Route responde 503 | Host sem Route, ou Route sem endpoints | `oc get route`; endpoints do Service |
| Hostname da Route inesperado | Sem `--hostname`: `<route>-<projeto>.<apps>` | `oc get route` |
| Job não termina / muitos Pods com erro | Comando falhando; `backoffLimit` | `oc get jobs`; `oc logs job/<j>` |
| CronJob roda no horário "errado" | Fuso do controller | Definir `spec.timeZone` |
| `oc delete all` deixou PVC/Secret | `all` é subconjunto | `oc api-resources --categories=all` |
| Banco recém-implantado em `CrashLoopBackOff` | Variáveis obrigatórias ausentes | `oc logs`; `oc set env deployment/<d> ...` |
| Sticky session não funciona | Route passthrough | Usar edge/re-encrypt |

## Configuração e storage ([5.1](../capitulos/05-configuracao-e-storage/5.1-externalizar-configuracao.md)–[5.7](../capitulos/05-configuracao-e-storage/5.7-storage-nao-compartilhado-com-statefulsets.md))

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| `CreateContainerConfigError` | ConfigMap/Secret ou chave inexistente | `oc describe pod`; `oc get cm,secret` |
| Variável com valor antigo após `oc set data` | Variáveis só são lidas no start | `oc rollout restart deployment/<d>` |
| Arquivo montado não atualiza | `subPath` ou aplicação lê só no start | Reiniciar; evitar `subPath` |
| Volume "apagou" arquivos da imagem | Montagem sobrepõe o diretório | Montar em outro caminho |
| PVC `Pending` | Classe inexistente, sem padrão, sem PV compatível, ou `WaitForFirstConsumer` | `oc describe pvc`; `oc get sc` |
| Réplicas em `ContainerCreating` com mesmo PVC | RWO em nós diferentes | RWX ou StatefulSet |
| Expansão de PVC não acontece | `allowVolumeExpansion` falso ou storage não atende | `oc describe pvc`; reduzir pedido (≥ capacidade atual) |
| PVC apagado continua `Terminating` | Pod ainda usa o PVC (protection) | Remover o volume do workload |
| PV `Released` não reaproveitado | `Retain` exige ação manual | Admin: backup do YAML, apagar e recriar PV |
| Pods do StatefulSet sem DNS por Pod | Headless Service ausente ou seletor errado | `oc get svc` (`CLUSTER-IP None`); labels |
| Dados "voltaram" após recriar StatefulSet | PVCs permanecem | `oc get pvc` |

## Confiabilidade ([6.3](../capitulos/06-confiabilidade/6.3-health-probes.md)–[6.9](../capitulos/06-confiabilidade/6.9-autoscaling-de-aplicacoes.md))

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| Pod `Running`, `READY 0/1` | Readiness falhando (caminho/porta, dependência) | `oc describe pod` (`Readiness probe failed`) |
| Reinícios em loop com `Liveness probe failed` | Aplicação lenta sem startup probe; limites curtos | Adicionar startup; ajustar `failureThreshold`/`periodSeconds` |
| Erros para clientes durante escala ou rollout | Sem readiness | `oc set probe --readiness` |
| Pod travado continua recebendo tráfego | Sem liveness/readiness | Configurar probes |
| `Pending` com `Insufficient memory/cpu` | Soma de requests excede o allocatable | `oc describe node`; revisar requests |
| `OOMKilled`, exit 137 | Limit de memória atingido (vazamento ou limit pequeno) | `oc describe pod` (Last State); `oc adm top pods` |
| Aplicação lenta com CPU livre no nó | Throttling por limit de CPU | `oc adm top pods` próximo do limit |
| Runtime antigo com OOM inesperado | Sem suporte a cgroups v2 | Atualizar imagem (OpenJDK 8u372+, Node.js 22+, .NET 5+) |
| `oc set resources` recusa `1gi` | Sufixo inválido | Usar `1Gi` |
| HPA `<unknown>` persistente | Sem request para a métrica | `oc set resources --requests` |
| HPA não passa de N réplicas | `maxReplicas` ou falta de capacidade | `oc describe hpa`; Pods `Pending` |
| Valor de resize "sumiu" | Novo Pod criado a partir do template | Atualizar o Deployment |

## Atualizações ([7.1](../capitulos/07-atualizacao-aplicacoes/7.1-identidade-e-tags-de-imagens.md)–[7.7](../capitulos/07-atualizacao-aplicacoes/7.7-triggers-de-mudanca-de-imagem.md))

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| Réplicas com `imageID` diferentes | Tag flutuante + `IfNotPresent` | `.status.containerStatuses[].imageID`; usar digest/ImageStream |
| `oc image info`: *manifest list* | Imagem multiarquitetura | `--filter-by-os linux/amd64` |
| Rollout parado / `ProgressDeadlineExceeded` | Imagem errada, readiness falhando | `oc rollout status`; `oc get pods`; `oc rollout undo` |
| Erros durante rollout | Sem readiness | `oc set probe --readiness` |
| Vários rollouts para várias mudanças | Trigger de configuração ativo | `oc rollout pause` / `resume` |
| Rollback trouxe imagem diferente | Tag flutuante mudou no registry | Usar digest ou ImageStream |
| Nome curto em `ImagePullBackOff` | Sem lookup local ou IS em outro projeto | `oc set image-lookup` |
| istag não recebe imagem nova da origem | Sem `--scheduled` (padrão) | `oc tag ... --scheduled` ou atualizar manualmente |
| Tag mudou e Deployment não | Sem trigger, `--manual` ou Deployment pausado | `oc set triggers deployment/<d>` |
| `oc rollout undo` desfeito | Image trigger reaplica a imagem da tag | Reverter a istag/alias |
| Disco de imagens cheio no nó | GC só age acima de 85% | `crictl imagefsinfo`; `KubeletConfig` |

## Aplicações (prévia)

| Sintoma | Causa provável | Como verificar |
|---------|----------------|----------------|
| Pod `Pending` | Sem nó com recursos, PVC não atendido | `oc describe pod` (eventos) |
| `ImagePullBackOff` | Nome/tag errado, registry inacessível, falta de credencial | `oc describe pod` |
| `CrashLoopBackOff` | Aplicação termina logo após iniciar | `oc logs <pod> --previous` |
| Route responde 503 | Service sem endpoints | `oc describe svc`; comparar selector com `oc get pods --show-labels` |
| PVC `Pending` | Classe inexistente, sem padrão ou `WaitForFirstConsumer` | `oc describe pvc`; `oc get storageclass` |
| Correção manual no Pod "sumiu" | Pod recriado a partir da configuração | Corrigir no Deployment/ConfigMap |

---
[← Exemplos YAML](exemplos-yaml.md) | [Início](../README.md) | [Glossário →](glossario.md)
