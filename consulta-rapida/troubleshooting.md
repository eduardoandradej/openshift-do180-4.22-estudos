# Troubleshooting: sintoma → causa → verificação

> Cobertura atual: fundamentos e Capítulo 1. Ampliado nos capítulos 2, 3, 4 e 6.

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
| Alerta disparando | Condição de regra atingida | Observe › Alerting › regra (descrição e expressão) |

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
