# Revisão — Capítulo 2

Questões **autorais**. Elas não reproduzem o quiz oficial nem perguntas de exame.
Tente responder no terminal, em cluster próprio ou com um `lab start` ativo,
antes de abrir as respostas.

## Parte 1 — Conceitos

1. Por que se diz que o `oc` é um superconjunto do `kubectl`? Cite três comandos que só existem no `oc`.
2. Explique a diferença entre `401 Unauthorized` e `403 Forbidden` usando o fluxo de uma requisição.
3. Qual método de login é o mais confiável em qualquer cluster e por quê?
4. O que é uma ServiceAccount e por que ela existe?
5. Qual a diferença entre `spec` e `status`? O que são *conditions*?
6. Qual a diferença entre o CVO e o OLM?
7. Explique `capacity` × `allocatable` em um nó. Qual dos dois o scheduler usa?

## Parte 2 — Comandos (escreva o comando)

8. Listar os tipos de recurso de escopo de cluster, só com os nomes, e contá-los.
9. Listar os tipos do grupo `route.openshift.io`.
10. Documentar o campo `spec.replicas` de um Deployment.
11. Mostrar nome, nó e IP de todos os Pods do projeto em uma tabela personalizada.
12. Mostrar só as conditions do cluster operator `dns`.
13. Mostrar o consumo por container de um Pod `db-0` no namespace `banco`.
14. Listar os eventos de todos os namespaces em ordem cronológica.
15. Ver as 10 últimas linhas do log do `crio` no nó `worker-2`.
16. Abrir uma cópia de depuração do Deployment `api` executando como o UID 1001.
17. Coletar dados de depuração do cluster operator `ingress` da última hora em `~/inspect-ingress`.

## Parte 3 — Diagnóstico

18. `oc get nodes` mostra `worker-3 NotReady`. Descreva três verificações em ordem.
19. Um script de inventário usa `oc describe` e quebrou após a atualização do cluster. O que mudar?
20. `oc logs app-xyz` retorna erro pedindo para escolher um container. O que acontece e como resolver?

---

<details>
<summary>Respostas comentadas</summary>

1. O `oc` contém todos os comandos do `kubectl` (mesma sintaxe) e acrescenta comandos para recursos e fluxos do OpenShift. Exemplos: `oc login`, `oc new-project`, `oc new-app`, `oc project`, `oc adm ...`.
2. Primeiro a **autenticação** identifica o usuário; se falhar, `401`. Depois a **autorização** verifica se aquele usuário pode executar a ação; se não puder, `403`.
3. **Token.** Funciona em qualquer cluster, inclusive quando o login por formulário é substituído por SSO, e não exige guardar senhas em scripts.
4. Conta usada por **aplicações** para acessar a API sem usar credenciais de pessoas. Cada projeto recebe service accounts automaticamente.
5. `spec` é o estado desejado (escrito por você); `status` é o estado atual (escrito pelos controllers). Conditions são entradas do `status` com `type`, `status`, `reason`, `message` e `lastTransitionTime`, que explicam o estado.
6. O CVO gerencia os **cluster operators** (plataforma, instalados por padrão); o OLM gerencia **operators adicionais** instalados pelo administrador.
7. `capacity` é o total do nó; `allocatable` é o disponível para Pods após as reservas do sistema. O scheduler usa **allocatable**.
8. `oc api-resources --namespaced=false -o name | wc -l`
9. `oc api-resources --api-group route.openshift.io`
10. `oc explain deployment.spec.replicas`
11. `oc get pods -o custom-columns=POD:.metadata.name,NO:.spec.nodeName,IP:.status.podIP` (ou `oc get pods -o wide`).
12. `oc get co dns -o jsonpath='{.status.conditions}' | jq` (ou `oc get co dns -o json | jq .status.conditions`).
13. `oc adm top pods db-0 -n banco --containers`
14. `oc get events -A --sort-by .metadata.creationTimestamp`
15. `oc adm node-logs worker-2 -u crio --tail 10`
16. `oc debug deployment/api --as-user=1001`
17. `oc adm inspect clusteroperator/ingress --since 1h --dest-dir ~/inspect-ingress`
18. (a) `oc describe node worker-3`: conditions (`Ready`, pressões, `NetworkUnavailable`) e eventos; (b) `oc adm node-logs worker-3 -u kubelet --tail 50`; (c) `oc debug node/worker-3` → `chroot /host` → `systemctl status kubelet crio`. Se o nó não responde, o debug pod não sobe: os logs e o acesso à infraestrutura são o caminho.
19. Trocar `describe` (formato para humanos, instável) por `oc get -o json|jsonpath|custom-columns`, que são formatos estáveis.
20. O Pod tem mais de um container. Liste os containers com `oc get pod app-xyz -o jsonpath='{.spec.containers[*].name}'` e use `oc logs app-xyz -c <container>`.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 18–20 | Siga para o Capítulo 3 |
| 14–17 | Refaça a Parte C das lições onde errou |
| < 14 | Repita os guided exercises e registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
