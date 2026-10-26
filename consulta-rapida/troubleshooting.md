# Troubleshooting: sintoma → causa → verificação

> Cobertura atual: fundamentos e Capítulos 1–3. Ampliado nos capítulos 4 e 6.

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
