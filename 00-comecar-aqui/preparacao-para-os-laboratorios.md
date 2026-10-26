# Preparação para os laboratórios

| Campo | Valor |
|-------|-------|
| Referência | Capítulo 0 — *Performing Lab Exercises*, PDF p. 12–14 |

## Tipos de atividade

| Tipo | Como funciona | `lab grade`? |
|------|---------------|--------------|
| **Matching / Quiz** | Verificação de conhecimento, quando a prática não é viável ou necessária | Não |
| **Guided Exercise** | Prática passo a passo logo após uma seção conceitual | Não |
| **Lab de fim de capítulo** | Passos de alto nível baseados nos guided exercises do capítulo, sem cada comando; há solução comentada | Sim (avaliável)* |
| **Comprehensive Review** (Cap. 8) | Você recebe uma **especificação** do resultado, sem os passos; pode cobrir o curso inteiro | Sim |

\* Regra geral do curso: **somente labs de fim de capítulo e comprehensive reviews
aceitam `grade`**. Exceção observada: o lab 1.9 (`intro-review`) é verificado pelo
quiz 1.10 e o PDF não indica `lab grade` para ele. Cada `PRATICA-OFICIAL.md`
registra o que foi verificado.

## O comando `lab`

Formato: `lab <ação> <atividade>`, executado no `workstation` como `student`.

| Ação | O que faz |
|------|-----------|
| `start` | Verifica e prepara os recursos: ajusta configurações, cria recursos, confirma serviços e resultados exigidos de atividades anteriores. Permite fazer qualquer atividade **sem ter feito as anteriores** |
| `grade` | Avalia o trabalho e lista critérios com `PASS`/`FAIL`. Corrija os `FAIL` e rode de novo |
| `finish` | Limpa os recursos da atividade. A atividade pode ser repetida quantas vezes quiser |

Regras importantes:

- **Uma atividade ativa por vez.** Se outra estiver em andamento, o `lab` pede para finalizá-la antes.
- **Tab completion:** `lab start` + Tab duas vezes lista as atividades disponíveis.
- Cada `lab start` **cria um projeto OpenShift específico** da atividade; o `lab finish` o remove.
- `lab status` mostra o estado das atividades.

## Diretórios e logs

| Caminho | Conteúdo |
|---------|----------|
| `/home/student/DO180` | Workspace do curso |
| `/home/student/DO180/labs/<atividade>` | Arquivos copiados pelo `lab start` para aquela atividade |
| `/tmp/log/labs/` | Um log por atividade, útil quando um `lab start`/`finish` falha |
| `/home/student/.grading/config.yaml` | Configuração do curso usada pelo `lab`; não altere |

## Problemas conhecidos de rotina

| Sintoma | Causa | O que fazer |
|---------|-------|-------------|
| `lab start` falha ao verificar a API ou as credenciais logo após criar o ambiente | O cluster pode levar **até 15 minutos** para ficar disponível | `lab finish <atividade>`, aguardar alguns minutos, `lab start` de novo |
| `lab start` falha ao repetir uma atividade | O projeto da execução anterior ainda está sendo removido (pode levar **até 10 minutos**) | Aguardar e tentar novamente |
| `lab start` recusa iniciar | Outra atividade está ativa | `lab finish` da atividade ativa |
| `oc` responde `Unauthorized` | Sessão expirada | Refazer `oc login` |
| Recurso "não existe" | Projeto errado | `oc project` para conferir |
| Console mostra menos itens que o esperado | Logado como usuário comum | Conferir o usuário no canto superior direito |

## Checklist de execução

**Antes**
- [ ] Li as lições da seção e o `PRATICA-OFICIAL.md` do capítulo.
- [ ] Sei explicar cada objeto que a atividade vai criar ou inspecionar.
- [ ] `lab start <atividade>` terminou sem erro.

**Durante**
- [ ] Leio a saída de cada comando antes de seguir.
- [ ] Verifico cada mudança (`oc get`, `oc describe`, console).
- [ ] Se travar, volto à Parte C da lição antes de abrir a solução.
- [ ] Como administrador, observo sem alterar componentes da plataforma.

**Depois**
- [ ] `lab grade <atividade>` com tudo `PASS` (quando aplicável).
- [ ] `lab finish <atividade>` executado.
- [ ] Registro no [diário de laboratórios](../progresso/diario-de-laboratorios.md).
- [ ] Dificuldades anotadas em [dificuldades-identificadas.md](../progresso/dificuldades-identificadas.md).

---
[← Ambiente oficial](ambiente-oficial-red-hat.md) | [Índice](README.md) | [Próximo: Fundamentos essenciais →](../01-fundamentos-essenciais/README.md)
