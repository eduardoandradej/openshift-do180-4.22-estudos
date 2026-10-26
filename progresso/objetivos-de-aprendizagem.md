# Objetivos de aprendizagem e relação com o EX280

## Como ler este arquivo

| Marca | Significado |
|-------|-------------|
| ✅ **Confirmado** | Verificado em fonte oficial (PDF do curso) |
| 🔎 **A confirmar** | Baseado na estrutura pública conhecida do EX280; **conferir** na página oficial do exame antes de usar como referência |
| ➕ **Complementar** | Assunto que ajuda na prática, mas não é objetivo declarado |

> Não há aqui perguntas reais de exame nem promessa de correspondência com
> questões específicas. O EX280 é prático e baseado em desempenho.
>
> Página oficial: <https://www.redhat.com/en/services/training/red-hat-certified-openshift-administrator-exam>.
> Na sessão em que este arquivo foi criado, a página não pôde ser consultada
> (rede restrita). Por isso as áreas do EX280 estão marcadas como 🔎.

## 1. Objetivos do DO180 (✅ confirmados — PDF p. 8)

| # | Objetivo do curso (linguagem própria) | Capítulos | Estudado? |
|---|---------------------------------------|-----------|-----------|
| 1 | Gerenciar clusters pela CLI e pela web console | 1, 2 | [ ] |
| 2 | Implantar aplicações a partir de imagens, templates e manifestos | 3, 4 | [ ] |
| 3 | Diagnosticar conectividade de rede entre aplicações, dentro e fora do cluster | 4 | [ ] |
| 4 | Conectar workloads a armazenamento | 5 | [ ] |
| 5 | Configurar workloads para alta disponibilidade e confiabilidade | 6 | [ ] |
| 6 | Gerenciar atualizações de imagens, configurações e manifestos | 7 | [ ] |

## 2. Áreas do EX280 × DO180 / DO280 (🔎 a confirmar)

| Área do EX280 (estrutura pública conhecida) | Coberta no DO180 | Coberta no DO280 |
|---------------------------------------------|------------------|------------------|
| Gerenciar o OpenShift Container Platform (console, CLI, consultar e filtrar recursos, diagnosticar) | Cap. 1, 2, 3 | Reforço |
| Implantar aplicações (recursos, manifestos, Deployments, exposição) | Cap. 3, 4 | Templates/Helm |
| Gerenciar storage para dados de aplicação | Cap. 5 | — |
| Configurar aplicações para confiabilidade (probes, recursos, autoscaling) | Cap. 6 | — |
| Gerenciar atualizações de aplicações (imagens, ImageStreams, triggers) | Cap. 7 | — |
| Gerenciar autenticação e autorização (provedores de identidade, RBAC) | — | Sim |
| Configurar segurança de rede (NetworkPolicy, TLS em Routes) | Introdução (Routes) | Sim |
| Habilitar self-service de desenvolvedores (quotas, limit ranges, templates de projeto) | — | Sim |
| Gerenciar Operators | Conceito (Cap. 1) | Sim |
| Configurar segurança de aplicações (SCC, service accounts, Secrets) | Secrets (Cap. 5) | Sim |

## 3. Competências do Capítulo 1 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Descrever containers, Pods e o modelo declarativo do Kubernetes | [1.1](../capitulos/01-introducao-kubernetes-openshift/1.1-containers-e-kubernetes.md) | Base conceitual (🔎) |
| Relacionar OpenShift, Kubernetes, edições e ciclo de vida (EUS) | [1.3](../capitulos/01-introducao-kubernetes-openshift/1.3-componentes-e-edicoes-do-openshift.md) | ➕ Contexto |
| Navegar na web console e localizar recursos | [1.5](../capitulos/01-introducao-kubernetes-openshift/1.5-navegar-na-web-console.md) | Uso da console (🔎) |
| Monitorar nós, Pods, métricas, alertas e eventos | [1.7](../capitulos/01-introducao-kubernetes-openshift/1.7-monitorar-um-cluster-openshift.md) | Diagnóstico (🔎) |
| Equivalentes de CLI (`oc whoami --show-console`, `oc debug node`, `oc get events`) | 1.5 e 1.7 | ➕ Velocidade no exame prático |

## 4. Competências do Capítulo 2 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Instalar/obter `oc` e `kubectl` compatíveis; entender a regra de ±1 minor | [2.1](../capitulos/02-cli-e-apis/2.1-interfaces-de-linha-de-comando.md) | ➕ Contexto |
| Autenticar por senha, token e `--web`; trabalhar com projetos e `-n` | 2.1 | Uso da CLI (🔎) |
| Descobrir tipos e campos (`api-resources`, `explain`) | [2.3](../capitulos/02-cli-e-apis/2.3-inspecionar-recursos-kubernetes.md) | Consultar recursos sem documentação externa (🔎) |
| Formatar e filtrar saídas (`-o yaml/json/jsonpath/custom-columns`, `jq`) | 2.3 | Consultar, formatar e filtrar atributos (🔎) |
| Avaliar operators, nós, Pods, métricas, eventos e alertas | [2.5](../capitulos/02-cli-e-apis/2.5-avaliar-a-saude-do-cluster.md) | Diagnóstico de cluster e aplicações (🔎) |
| Coletar dados para suporte (`must-gather`, `inspect`) | 2.5 | Diagnóstico (🔎) |

## 5. Competências dos próximos capítulos

Serão adicionadas aqui à medida que cada PDF for recebido e cada capítulo validado.

---
[Início](../README.md) | [Estado do projeto](estado-do-projeto.md)
