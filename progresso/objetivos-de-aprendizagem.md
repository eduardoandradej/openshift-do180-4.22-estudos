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

## 5. Competências do Capítulo 3 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Criar Pods com `oc run`, controlar comando, variáveis e reinício | [3.1](../capitulos/03-containers-e-pods/3.1-criar-containers-e-pods.md) | Implantar e testar aplicações (🔎) |
| Entender UIDs por projeto, GID 0, PSA e SCC | 3.1 | Base para segurança de aplicações (🔎, aprofundado no DO280) |
| Inspecionar o container no nó (`crictl`, `lsns`, `nsenter`) | 3.1 | ➕ Diagnóstico avançado |
| Encontrar e inspecionar imagens (`skopeo`, `oc image`) | [3.3](../capitulos/03-containers-e-pods/3.3-encontrar-e-inspecionar-imagens.md) | Escolher e validar imagens (🔎) |
| Diagnosticar Pods: logs, eventos, exec, cp, port-forward, edit/patch | [3.5](../capitulos/03-containers-e-pods/3.5-diagnosticar-containers-e-pods.md) | Diagnóstico de aplicações (🔎) |

## 6. Competências do Capítulo 4 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Implantar a partir de imagem, Git e template (`oc new-app`, `oc process`) | [4.1](../capitulos/04-deploy-e-redes/4.1-implantar-a-partir-de-imagem-e-template.md) | Implantar aplicações (🔎) |
| Gerar e aplicar manifestos (imperativo → declarativo) | 4.1 | Implantar com manifestos (🔎) |
| Escolher e criar Job, CronJob, Deployment, DaemonSet | [4.3](../capitulos/04-deploy-e-redes/4.3-workloads-de-longa-e-curta-duracao.md) | Implantar aplicações (🔎) |
| Criar Services, verificar seletores e endpoints, usar o DNS interno | [4.5](../capitulos/04-deploy-e-redes/4.5-redes-de-pods-e-services.md) | Conectividade e diagnóstico (🔎) |
| Expor com Route/Ingress, sessões persistentes, escalar | [4.7](../capitulos/04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md) | Expor aplicações (🔎) |
| Conhecer a Gateway API e os tipos de Service | 4.7 | ➕ Contexto (aprofundar no DO280) |

## 7. Competências do Capítulo 5 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Criar ConfigMaps e Secrets e consumi-los como variáveis e arquivos | [5.1](../capitulos/05-configuracao-e-storage/5.1-externalizar-configuracao.md) | Configurar aplicações (🔎) |
| Atualizar configuração (`extract`, `set data`) e reiniciar quando necessário | 5.1 | Configurar aplicações (🔎) |
| Provisionar PVCs, montar em Deployments, expandir | [5.3](../capitulos/05-configuracao-e-storage/5.3-provisionar-volumes-persistentes.md) | Gerenciar storage (🔎) |
| Escolher StorageClass pelos requisitos (acesso, modo, reclaim, binding) | [5.5](../capitulos/05-configuracao-e-storage/5.5-selecionar-storage-class.md) | Gerenciar storage (🔎) |
| Implantar StatefulSets com headless Service e PVC por réplica | [5.7](../capitulos/05-configuracao-e-storage/5.7-storage-nao-compartilhado-com-statefulsets.md) | Gerenciar storage e implantar aplicações (🔎) |

## 8. Competências do Capítulo 6 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Explicar os mecanismos de HA (restart, controllers, probes, escala) | [6.1](../capitulos/06-confiabilidade/6.1-alta-disponibilidade-de-aplicacoes.md) | Confiabilidade (🔎) |
| Configurar probes startup, readiness e liveness | [6.3](../capitulos/06-confiabilidade/6.3-health-probes.md) | Confiabilidade (🔎) |
| Definir requests e diagnosticar `FailedScheduling` | [6.5](../capitulos/06-confiabilidade/6.5-reservar-capacidade-de-computacao.md) | Confiabilidade (🔎) |
| Definir limits, diagnosticar `OOMKilled`/throttling, redimensionar no local | [6.7](../capitulos/06-confiabilidade/6.7-limitar-capacidade-de-computacao.md) | Confiabilidade (🔎) |
| Criar e acompanhar HPA (CPU e memória); conhecer o VPA | [6.9](../capitulos/06-confiabilidade/6.9-autoscaling-de-aplicacoes.md) | Confiabilidade (🔎) |

## 9. Competências do Capítulo 7 (✅ confirmadas no PDF)

| Competência | Lição | Relevância para EX280 |
|-------------|-------|-----------------------|
| Relacionar tags e digests; escolher `imagePullPolicy` | [7.1](../capitulos/07-atualizacao-aplicacoes/7.1-identidade-e-tags-de-imagens.md) | Atualizações de aplicações (🔎) |
| Atualizar imagem e configuração com estratégias, pause/resume e rollback | [7.3](../capitulos/07-atualizacao-aplicacoes/7.3-atualizar-imagem-e-configuracoes.md) | Atualizações de aplicações (🔎) |
| Criar e usar ImageStreams e ImageStreamTags | [7.5](../capitulos/07-atualizacao-aplicacoes/7.5-implantacoes-reproduziveis-com-imagestreams.md) | Atualizações de aplicações (🔎) |
| Configurar image triggers e promover/reverter com aliases | [7.7](../capitulos/07-atualizacao-aplicacoes/7.7-triggers-de-mudanca-de-imagem.md) | Atualizações de aplicações (🔎) |

## 10. Capítulo 8 — revisão integrada (✅ confirmada no PDF)

O curso declara que a revisão do Capítulo 8 apoia a preparação para os exames
**EX180** e **EX280** (PDF p. 495). Os dois labs cobram, por especificação e com
tempo, as competências dos capítulos 4 a 7 (e a observação dos capítulos 1 e 2).
Treino autoral equivalente em [REVISAO.md do Capítulo 8](../capitulos/08-revisao-geral/REVISAO.md).

## 11. Lacunas para o EX280 (cobertas no DO280)

| Área | Situação após o DO180 |
|------|-----------------------|
| Provedores de identidade, usuários e grupos | Não coberto |
| RBAC (roles, bindings) | Não coberto |
| SCC e service accounts | Apenas mencionado (Cap. 3) |
| NetworkPolicy e TLS em Routes | Routes básicas apenas (Cap. 4) |
| Quotas, LimitRanges e templates de projeto | LimitRange apenas mencionado (Cap. 6) |
| Operators (OLM) | Apenas conceito e consulta (Caps. 1 e 2) |

---
[Início](../README.md) | [Estado do projeto](estado-do-projeto.md)
