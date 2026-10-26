# Exemplos originais

Manifestos **autorais** para leitura e para testes em clusters próprios (OpenShift
Local, Developer Sandbox). Não são soluções dos exercícios oficiais e não devem
ser aplicados no ambiente de laboratório durante uma atividade.

| Arquivo | Conteúdo | Lição relacionada |
|---------|----------|-------------------|
| [web-deployment-service-route.yaml](web-deployment-service-route.yaml) | Deployment + Service + Route mínimos | [F4](../01-fundamentos-essenciais/04-pods-e-workloads.md), [F6](../01-fundamentos-essenciais/06-redes-e-servicos.md) |
| [pvc-basico.yaml](pvc-basico.yaml) | PVC usando a StorageClass padrão | [F7](../01-fundamentos-essenciais/07-persistencia-de-dados.md) |

Uso sugerido em cluster próprio:

```bash
oc new-project exemplos
oc apply -f exemplos-originais/web-deployment-service-route.yaml --dry-run=server
oc apply -f exemplos-originais/web-deployment-service-route.yaml
oc get deployment,pod,svc,route
oc delete project exemplos
```

Regras: nenhum Secret real, nenhuma credencial e nenhum nome de host do ambiente
oficial.

---
[Início](../README.md)
