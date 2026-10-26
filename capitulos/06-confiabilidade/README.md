# Capítulo 6 — Configure Applications for Reliability

**Título em português:** Configurar aplicações para confiabilidade
**Status:** ✅ concluído e validado
**Referência:** PDF p. 377–436

## Objetivo do capítulo

Configurar as aplicações para que trabalhem **junto com o Kubernetes** e obtenham
alta disponibilidade e resiliência.

## Por que este capítulo importa

Até aqui as aplicações rodam, se comunicam e guardam dados. Agora elas precisam
**continuar funcionando** diante de falhas, de inicializações lentas, de vizinhos
famintos e de picos de carga. Probes, requests, limits e autoscaling são
configurações do dia a dia do administrador e aparecem com frequência em
diagnósticos e no EX280.

```mermaid
flowchart LR
    A[6.1 HA<br/>restart · controllers] --> B[6.3 Probes<br/>startup · readiness · liveness]
    B --> C[6.5 Requests<br/>agendamento · allocatable]
    C --> D[6.7 Limits<br/>OOMKilled · throttling · resize]
    D --> E[6.9 Autoscaling<br/>HPA · VPA]
    E --> F[6.11 Lab + 6.12 Quiz]
    F --> G[Capítulo 7<br/>Atualizações]
```

## Seções e atividades (ordem oficial)

| Seção | Tipo | Título original | Material | PDF |
|-------|------|-----------------|----------|-----|
| 6.1 | Conceito | Application High Availability with Kubernetes | [lição](6.1-alta-disponibilidade-de-aplicacoes.md) | p. 378–379 |
| 6.2 | Guided Exercise | Application High Availability with Kubernetes | [prática](PRATICA-OFICIAL.md#62-guided-exercise-application-high-availability-with-kubernetes) | p. 380–385 |
| 6.3 | Conceito | Application Health Probes | [lição](6.3-health-probes.md) | p. 386–390 |
| 6.4 | Guided Exercise | Application Health Probes | [prática](PRATICA-OFICIAL.md#64-guided-exercise-application-health-probes) | p. 391–396 |
| 6.5 | Conceito | Reserving Compute Capacity for Applications | [lição](6.5-reservar-capacidade-de-computacao.md) | p. 397–400 |
| 6.6 | Guided Exercise | Reserving Compute Capacity for Applications | [prática](PRATICA-OFICIAL.md#66-guided-exercise-reserving-compute-capacity-for-applications) | p. 401–404 |
| 6.7 | Conceito | Limit Compute Capacity for Applications | [lição](6.7-limitar-capacidade-de-computacao.md) | p. 405–411 |
| 6.8 | Guided Exercise | Limit Compute Capacity for Applications | [prática](PRATICA-OFICIAL.md#68-guided-exercise-limit-compute-capacity-for-applications) | p. 412–414 |
| 6.9 | Conceito | Application Autoscaling | [lição](6.9-autoscaling-de-aplicacoes.md) | p. 415–419 |
| 6.10 | Guided Exercise | Application Autoscaling | [prática](PRATICA-OFICIAL.md#610-guided-exercise-application-autoscaling) | p. 420–425 |
| 6.11 | Lab | Configure an Application for Reliability | [prática](PRATICA-OFICIAL.md#611-lab-configure-an-application-for-reliability) | p. 426–433 |
| 6.12 | Quiz | Configure an Application for Reliability | [prática](PRATICA-OFICIAL.md#612-quiz-configure-an-application-for-reliability) | p. 434–435 |
| 6.13 | Summary | Summary | [RESUMO.md](RESUMO.md) | p. 436 |

## Arquivos do capítulo

- [PRATICA-OFICIAL.md](PRATICA-OFICIAL.md): ponte com as atividades oficiais.
- [REVISAO.md](REVISAO.md): questões autorais integradas.
- [RESUMO.md](RESUMO.md): síntese e tabela de comandos.

## Pré-requisitos recomendados

[Capítulo 4](../04-deploy-e-redes/README.md) ·
[2.5 — Saúde do cluster](../02-cli-e-apis/2.5-avaliar-a-saude-do-cluster.md) ·
[F1 — cgroups](../../01-fundamentos-essenciais/01-containers-e-imagens.md)

## Checklist

- [ ] 6.1 lida e Parte F respondida
- [ ] 6.2 Guided Exercise `reliability-ha` concluído
- [ ] 6.3 lida e Parte F respondida
- [ ] 6.4 Guided Exercise `reliability-probes` concluído
- [ ] 6.5 lida e Parte F respondida
- [ ] 6.6 Guided Exercise `reliability-requests` concluído
- [ ] 6.7 lida e Parte F respondida
- [ ] 6.8 Guided Exercise `reliability-limits` concluído
- [ ] 6.9 lida e Parte F respondida
- [ ] 6.10 Guided Exercise `reliability-autoscaling` concluído
- [ ] 6.11 Lab `reliability-review` com `lab grade` aprovado
- [ ] 6.12 Quiz respondido
- [ ] [REVISAO.md](REVISAO.md) respondida
- [ ] Registro no [diário de laboratórios](../../progresso/diario-de-laboratorios.md)

---
[← Capítulo 5](../05-configuracao-e-storage/README.md) | [Índice geral](../../README.md) | [Próximo: 6.1 Alta disponibilidade →](6.1-alta-disponibilidade-de-aplicacoes.md)
