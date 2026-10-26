# Prática oficial — Capítulo 8

> Ponte para os laboratórios de revisão do curso. **Não** reproduz especificações,
> valores, respostas ou soluções. Execute tudo no ambiente oficial, no
> `workstation`, como `student`. As credenciais estão no enunciado.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | Tempo de referência | PDF |
|-------|------|---------------------|-------------|---------------------|-----|
| 8.1 | Revisão de objetivos | — | — | — | p. 496–497 |
| 8.2 | Lab (Comprehensive Review) | `compreview-deploy` | **Sim** | 35 min | p. 498–506 |
| 8.3 | Lab (Comprehensive Review) | `compreview-scale` | **Sim** | 20 min | p. 507–512 |

Identificadores, avaliação e tempos verificados no PDF do Capítulo 8.

**Como esses labs funcionam:** você recebe uma **especificação** do resultado, sem
passos. O `lab grade` traz **dicas de correção** que apontam o conteúdo a revisar.
O `lab start` deixa um arquivo `resources.txt` com URLs e nomes de imagens para
copiar. Se precisar de mais tempo que o de referência, o curso recomenda revisar e
praticar mais.

---

## 8.2 Lab: Deploy Web Applications

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `compreview-deploy` |
| Avaliação | **`lab grade compreview-deploy`** |
| Tempo de referência | 35 minutos |
| Referência | PDF p. 498–506 |

**Competências cobradas (resumo autoral):** implantar uma aplicação de duas camadas
(interface web + banco MariaDB) em um projeto novo, usando:

- **ImageStream** com nome curto, isolando os workloads de mudanças de registry ([7.5](../07-atualizacao-aplicacoes/7.5-implantacoes-reproduziveis-com-imagestreams.md));
- **Secret** consumido como variáveis pelo banco e pelo frontend, com **prefixo** no frontend ([5.1](../05-configuracao-e-storage/5.1-externalizar-configuracao.md));
- **volume persistente** com tamanho, caminho e StorageClass definidos ([5.3](../05-configuracao-e-storage/5.3-provisionar-volumes-persistentes.md), [5.5](../05-configuracao-e-storage/5.5-selecionar-storage-class.md));
- **image trigger** para reimplantar o banco quando a ImageStreamTag mudar ([7.7](../07-atualizacao-aplicacoes/7.7-triggers-de-mudanca-de-imagem.md));
- **Services** com portas especificadas e **Route** com hostname definido ([4.5](../04-deploy-e-redes/4.5-redes-de-pods-e-services.md), [4.7](../04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md)).

```bash
lab start compreview-deploy
lab grade compreview-deploy
lab finish compreview-deploy
```

**Pontos de atenção:**
- O enunciado indica que o prefixo de variáveis a partir de Secret deve ser feito pela **CLI** (`oc set env --from secret/... --prefix`), porque a console não oferece prefixo.
- O trigger deve apontar para o **nome do container** indicado.
- O Service do frontend tem porta própria: confira `port` × `targetPort`.
- O hostname da Route segue um formato específico: compare com o padrão `<route>-<projeto>.<apps>`.
- O próprio enunciado lembra que probes e limits ficam para o outro lab de revisão.

---

## 8.3 Lab: Troubleshoot and Scale Applications

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `compreview-scale` |
| Avaliação | **`lab grade compreview-scale`** |
| Tempo de referência | 20 minutos |
| Referência | PDF p. 507–512 |

**Competências cobradas (resumo autoral):** como administrador:

- usar a **console** para identificar um workload de outro projeto que consome CPU em excesso e removê-lo ([1.7](../01-introducao-kubernetes-openshift/1.7-monitorar-um-cluster-openshift.md), [2.5](../02-cli-e-apis/2.5-avaliar-a-saude-do-cluster.md));
- diagnosticar e corrigir um banco que não inicia ([3.5](../03-containers-e-pods/3.5-diagnosticar-containers-e-pods.md), [5.1](../05-configuracao-e-storage/5.1-externalizar-configuracao.md));
- atualizar a imagem do banco para uma versão validada ([7.3](../07-atualizacao-aplicacoes/7.3-atualizar-imagem-e-configuracoes.md));
- configurar **probes** por comando no banco e HTTP no frontend ([6.3](../06-confiabilidade/6.3-health-probes.md));
- definir **requests** e **limits** ([6.5](../06-confiabilidade/6.5-reservar-capacidade-de-computacao.md), [6.7](../06-confiabilidade/6.7-limitar-capacidade-de-computacao.md));
- **escalar** o frontend para alta disponibilidade ([4.7](../04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md)).

```bash
lab start compreview-scale
lab grade compreview-scale
lab finish compreview-scale
```

**Pontos de atenção:**
- Comece pelo que **impede** o funcionamento (Pod com falha), depois o que **melhora** (probes, recursos, escala).
- Use `oc rollout pause`/`resume` para agrupar mudanças e evitar rollouts em sequência.
- Probe de **readiness** = "pronto para receber requisições"; **liveness** = "verificar regularmente".
- Unidades: millicores (`m`) e `Mi`/`Gi`, com maiúsculas.

---

**Registro:** anote os tempos e as dicas do `lab grade` no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 8.1 Resumo dos objetivos](8.1-resumo-dos-objetivos-de-aprendizagem.md) | [Índice do capítulo](README.md) | [Próximo: Revisão integrada →](REVISAO.md)
