# Sobre o curso DO180 (4.22)

| Campo | Valor |
|-------|-------|
| Curso | Red Hat OpenShift Administration I: Operating a Production Cluster (DO180) |
| Versão | Red Hat OpenShift Container Platform 4.22 · Edição 1 |
| Referência | Capítulo 0 — Introduction, PDF p. 1–14 (sumário p. 3–5; introdução p. 8–14) |

## Foco do curso

O DO180 prepara administradores para o **dia a dia de workloads Kubernetes** em um
cluster OpenShift, em colaboração com desenvolvedores, DevOps, administradores de
sistemas e SREs. O foco são **aplicações típicas de usuário final**, acessadas por
interface web ou mobile, e suas dependências (bancos de dados, mensageria,
autenticação). A administração do cluster em si (autenticação, RBAC, segurança,
rede avançada) é tema do DO280.

## Objetivos oficiais, em linguagem própria

| # | Objetivo | Onde no curso |
|---|----------|---------------|
| 1 | Gerenciar clusters pela CLI e pela web console | Cap. 1 e 2 |
| 2 | Implantar aplicações a partir de imagens, templates e manifestos | Cap. 3 e 4 |
| 3 | Diagnosticar conectividade de rede entre aplicações, dentro e fora do cluster | Cap. 4 |
| 4 | Conectar workloads a armazenamento para dados de aplicação | Cap. 5 |
| 5 | Configurar workloads para alta disponibilidade e confiabilidade | Cap. 6 |
| 6 | Gerenciar atualizações de imagens, configurações e manifestos | Cap. 7 |

## Público-alvo

- Administradores de sistemas que vão manter clusters OpenShift e aplicações em containers.
- SREs que mantêm e diagnosticam aplicações em Kubernetes.
- Arquitetos que precisam entender os recursos de um cluster OpenShift.

## Pré-requisitos declarados

- **DO080** (*Containers, Kubernetes and Red Hat OpenShift Technical Overview*) ou conhecimento equivalente de containers Linux. O módulo [01 — Fundamentos essenciais](../01-fundamentos-essenciais/README.md) cobre essa base.
- Uso básico de Bash: manipular arquivos e processos e verificar configurações do sistema, como endereços de rede. A Red Hat sugere o RH104 para quem não tem essa base.

## Convenções da apostila

A apostila usa quatro tipos de destaque. Aqui no repositório eles aparecem como ⚠️ e 📘:

| Destaque | Significado | Consequência de ignorar |
|----------|-------------|-------------------------|
| References | Onde achar documentação externa | — |
| Note | Dica ou atalho | Nenhuma grave |
| Important | Detalhe fácil de perder (ex.: mudança só vale na sessão atual) | Frustração, sem perda de dados |
| Warning | Não ignore | Provável **perda de dados** |

## Estrutura oficial (sumário verificado)

| Cap. | Título original | Seções conceituais | Atividades |
|------|-----------------|--------------------|-----------|
| 1 | Introduction to Kubernetes and OpenShift | 1.1, 1.3, 1.5, 1.7 | 2 Matching, 2 GE, Lab, Quiz |
| 2 | Kubernetes and OpenShift Command-line Interfaces and APIs | 2.1, 2.3, 2.5 | 3 GE, Lab, Quiz |
| 3 | Run Applications as Containers and Pods | 3.1, 3.3, 3.5 | 3 GE, Lab, Quiz |
| 4 | Deploy Managed and Networked Applications on Kubernetes | 4.1, 4.3, 4.5, 4.7 | 4 GE, Lab |
| 5 | Manage Storage for Application Configuration and Data | 5.1, 5.3, 5.5, 5.7 | 4 GE, Lab |
| 6 | Configure Applications for Reliability | 6.1, 6.3, 6.5, 6.7, 6.9 | 5 GE, Lab, Quiz |
| 7 | Manage Application Updates | 7.1, 7.3, 7.5, 7.7 | 4 GE, Lab |
| 8 | Comprehensive Review | 8.1 | 2 Labs de revisão |

---
[← Comece aqui](README.md) | [Índice](README.md) | [Próximo: Como usar este repositório →](como-usar-este-repositorio.md)
