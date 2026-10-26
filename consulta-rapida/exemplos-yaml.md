# Exemplos YAML comentados

Todos autorais e validados sintaticamente. Arquivos aplicáveis em
[exemplos-originais/](../exemplos-originais/README.md).

## Estrutura de qualquer objeto

```yaml
apiVersion: <grupo>/<versão>   # ex.: apps/v1; o grupo core é só "v1"
kind: <Tipo>                   # ex.: Deployment
metadata:
  name: <nome>
  namespace: <projeto>         # omitido = projeto atual
  labels:
    app: <nome>
spec: {}                       # estado desejado (varia por tipo)
# status: escrito pelo cluster; nunca no seu manifesto
```

## Deployment + Service + Route

Ver [web-deployment-service-route.yaml](../exemplos-originais/web-deployment-service-route.yaml).
Pontos de leitura:

1. `spec.selector.matchLabels` do Deployment **igual** a `spec.template.metadata.labels`.
2. `spec.selector` do Service casa com os labels dos Pods.
3. `spec.to.name` da Route aponta para o **nome do Service**.
4. `port.targetPort` da Route pode usar o **nome** da porta do Service (`http`).

## PersistentVolumeClaim

Ver [pvc-basico.yaml](../exemplos-originais/pvc-basico.yaml) e [F7](../01-fundamentos-essenciais/07-persistencia-de-dados.md).

## Erros de YAML mais comuns

| Erro | Sintoma |
|------|---------|
| Tab na indentação | `found character that cannot start any token` |
| Lista mal indentada | Campo ignorado ou `unknown field` |
| `apiVersion` incompatível com `kind` | `no matches for kind "X" in version "Y"` |
| Número entre aspas em campo numérico | Erro de validação de tipo |

---
[← Objetos Kubernetes](objetos-kubernetes.md) | [Início](../README.md) | [Troubleshooting →](troubleshooting.md)
