# Revisão — Capítulo 1

Questões **autorais** que integram as quatro seções. Responda por escrito antes de
abrir as respostas. Elas não reproduzem o quiz oficial nem perguntas de exame.

## Parte 1 — Conceitos

1. Explique, em até três frases, a relação entre container, Kubernetes e OpenShift.
2. Por que se diz que o Kubernetes trabalha com **estado desejado**? Qual componente torna isso possível?
3. Classifique cada item como **horizontal** ou **vertical**: (a) passar de 2 para 6 réplicas; (b) aumentar a memória de um Pod de 512 MiB para 1 GiB sem reiniciá-lo; (c) adicionar nós ao cluster conforme a carga.
4. Qual a diferença entre um nó de control plane e um compute node? Por que normalmente se separam esses papéis?
5. Associe: RHEL CoreOS · Insights Operator · Quay · EUS → (i) dados para recomendações · (ii) SO imutável · (iii) suporte estendido em versões pares · (iv) registry privado do Platform Plus.

## Parte 2 — Cenários operacionais

6. Você recebeu do time de infraestrutura apenas `https://api.prod.exemplo:6443` e um usuário. Descreva os passos e comandos para abrir a web console.
7. Um colega diz que a console do 4.22 "está faltando a perspectiva Developer". Explique o que mudou e o que um administrador pode fazer.
8. O monitoramento mostra um alerta de severidade *Warning* sobre StorageClasses. Em que páginas da console você investigaria e em que ordem?
9. Você precisa confirmar que o kubelet de um nó está ativo. Descreva o caminho pela console e o equivalente pela CLI.
10. Um desenvolvedor corrigiu um problema editando um arquivo **dentro** de um Pod pela aba *Terminal*. No dia seguinte, o problema voltou. Explique o que aconteceu e qual seria a correção correta.
11. A equipe quer garantir que os nós recebam uma configuração de sistema operacional de forma consistente. Que recurso e que operador estão envolvidos, e em que ordem os nós são atualizados?

## Parte 3 — Console ↔ CLI

12. Preencha a coluna da CLI:

| Na console | Na CLI |
|------------|--------|
| Home › Projects | ? |
| Workloads › Pods (todos os namespaces) | ? |
| Networking › Routes | ? |
| Compute › Nodes | ? |
| Home › Events | ? |
| Home › API Explorer | ? |

---

<details>
<summary>Respostas comentadas</summary>

1. O container empacota a aplicação e roda como processo isolado. O Kubernetes orquestra containers (em Pods) em um cluster, de forma declarativa. O OpenShift é uma plataforma completa construída sobre a extensibilidade do Kubernetes (registry, builds, observabilidade, RHEL CoreOS, console).
2. O administrador descreve o resultado e o cluster converge para ele. Os **controllers** comparam continuamente desejado e observado e agem para eliminar diferenças.
3. (a) horizontal; (b) vertical (*in-place pod resize*, Kubernetes 1.35 / OpenShift 4.22); (c) horizontal, no nível de nós.
4. Control plane coordena (agendamento e estado da configuração); compute executa cargas de usuários. Separar melhora estabilidade, segurança e gerenciabilidade, porque uma carga de usuário não compete com os componentes que mantêm o cluster.
5. RHEL CoreOS → (ii); Insights Operator → (i); Quay → (iv); EUS → (iii).
6. `oc login -u <usuario> https://api.prod.exemplo:6443` e depois `oc whoami --show-console`; abrir a URL no navegador e escolher o provedor de identidade.
7. Desde o 4.19 a console usa a **perspectiva unificada (Core platform)**. O administrador pode reativar a Developer em *Administration › Cluster Settings › Configuration › Console › Customize*.
8. *Observe › Alerting* (alerta e regra: descrição e expressão) → *Storage › StorageClasses* (quais existem e qual é padrão) → *Home › Events* (mudanças recentes).
9. Console: *Compute › Nodes* › nó › *Terminal* › `chroot /host` › `systemctl status kubelet`. CLI: `oc debug node/<nó>` › `chroot /host` › `systemctl status kubelet`.
10. O Pod foi recriado (rollout, falha ou reagendamento) a partir da imagem e da configuração declaradas, e a mudança manual se perdeu. Corrige-se no objeto que gera o Pod (Deployment, ConfigMap, imagem).
11. **MachineConfig** declara a configuração; o **Machine Config Operator** a aplica e mantém, orquestrando por zona em ordem alfabética (label `topology.kubernetes.io/zone`).
12. `oc get projects` · `oc get pods -A` · `oc get routes` · `oc get nodes` · `oc get events --sort-by=.lastTimestamp` · `oc api-resources` / `oc explain <tipo>`.

</details>

## Autoavaliação

| Acertos | Ação |
|---------|------|
| 11–12 | Siga para o Capítulo 2 |
| 8–10 | Releia a Parte G das lições onde errou |
| < 8 | Refaça as lições e a Parte F de cada uma; registre em [dificuldades-identificadas.md](../../progresso/dificuldades-identificadas.md) |

---
[← Prática oficial](PRATICA-OFICIAL.md) | [Índice do capítulo](README.md) | [Próximo: Resumo →](RESUMO.md)
