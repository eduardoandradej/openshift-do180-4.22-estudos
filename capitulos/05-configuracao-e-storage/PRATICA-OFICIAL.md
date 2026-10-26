# Prática oficial — Capítulo 5

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial, no `workstation`, como `student`.
> As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 5.2 | Guided Exercise | `storage-configs` | Não | p. 307–316 |
| 5.4 | Guided Exercise | `storage-volumes` | Não | p. 328–335 |
| 5.6 | Guided Exercise | `storage-classes` | Não | p. 342–348 |
| 5.8 | Guided Exercise | `storage-statefulsets` | Não | p. 356–362 |
| 5.9 | Lab | `storage-review` | **Sim** | p. 363–375 |

Identificadores e avaliação verificados no PDF do Capítulo 5. O capítulo não tem quiz.

---

## 5.2 Guided Exercise: Externalize the Configuration of Applications

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `storage-configs` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 307–316 |

**Competência praticada:** implantar um servidor web, expô-lo, criar um ConfigMap a
partir de dois arquivos e montá-lo como volume no Deployment.

**Domine antes:** [5.1](5.1-externalizar-configuracao.md) (ConfigMap a partir de
arquivos, `oc set volume --type configmap`) e [4.7](../04-deploy-e-redes/4.7-escalar-e-expor-aplicacoes.md) (Route).

```bash
lab start storage-configs
lab finish storage-configs
```

**Pontos de atenção:**
- Montar um volume em um diretório **substitui** o conteúdo original daquele diretório no container.
- Cada chave do ConfigMap vira um arquivo com o nome da chave.
- Depois de mudar o Deployment, espere todas as réplicas ficarem disponíveis antes de testar.

---

## 5.4 Guided Exercise: Provision Persistent Data Volumes

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `storage-volumes` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 328–335 |

**Competência praticada:** implantar um banco com storage persistente via PVC e
identificar o PV e o provisionador por trás da aplicação.

**Domine antes:** [5.3](5.3-provisionar-volumes-persistentes.md) (`oc set volumes`, ciclo de vida, `oc get pvc/pv`).

```bash
lab start storage-volumes
lab finish storage-volumes
```

**Pontos de atenção:**
- O nome do PV ligado está em `spec.volumeName` do PVC.
- O provisionador aparece na StorageClass e em anotações do PV.
- Teste a persistência: recrie o Pod e confirme que os dados continuam.

---

## 5.6 Guided Exercise: Selecting a Storage Class for an Application

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `storage-classes` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 342–348 |

**Competência praticada:** implantar um banco com storage persistente baseado em
**bloco/local**, escolhendo essa classe em vez do storage de arquivos padrão.

**Domine antes:** [5.5](5.5-selecionar-storage-class.md) (classes, `WaitForFirstConsumer`, `--claim-class`).

```bash
lab start storage-classes
lab finish storage-classes
```

**Pontos de atenção:**
- Identifique qual classe é a **padrão** e qual atende ao requisito do exercício.
- Com `WaitForFirstConsumer`, o PVC fica `Pending` até o Pod ser agendado.
- Confira a coluna `STORAGECLASS` do PVC no final.

---

## 5.8 Guided Exercise: Manage Non-shared Storage with Stateful Sets

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `storage-statefulsets` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 356–362 |

**Competência praticada:** implantar um servidor web replicado com Deployment e
verificar que as réplicas **compartilham** um PV; implantar um MySQL replicado com
StatefulSet e verificar que **cada instância** tem seu PV.

**Domine antes:** [5.7](5.7-storage-nao-compartilhado-com-statefulsets.md) (headless Service, `volumeClaimTemplates`, ordem de criação).

```bash
lab start storage-statefulsets
lab finish storage-statefulsets
```

**Pontos de atenção:**
- Crie o headless Service **antes** do StatefulSet.
- Observe a criação **ordenada** dos Pods.
- Relacione cada Pod ao seu PVC (`oc describe pod` mostra o `ClaimName`).

---

## 5.9 Lab: Manage Storage for Application Configuration and Data

| Campo | Valor |
|-------|-------|
| Identificador `lab` | `storage-review` |
| Avaliação | **`lab grade storage-review`** |
| Referência | PDF p. 363–375 |

**Competência praticada (resumo autoral):** criar um Secret com as credenciais do
banco e um ConfigMap com um arquivo SQL; implantar um banco que recebe as variáveis
do Secret com prefixo e usa storage **local/bloco**; implantar e escalar uma
aplicação web que precisa de storage **compartilhado** (NFS); expor banco e
aplicação; montar e depois remover volumes; usar o volume compartilhado para levar
o arquivo SQL até o banco e carregar os dados.

**Domine antes:** as quatro lições e a [revisão](REVISAO.md).

```bash
lab start storage-review
lab grade storage-review
lab finish storage-review
```

**Pontos de atenção:**
- O enunciado define **nomes**, **classes**, **modos de acesso**, **tamanhos** e **caminhos** exatos: o `lab grade` confere cada um.
- Escolha a classe de acordo com o requisito: arquivo compartilhado para várias réplicas; bloco/local para o banco.
- `oc set env --from secret/... --prefix ...` converte as chaves em maiúsculas.
- Para remover um volume, use o **nome do volume**, não o do PVC.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 5.7 StatefulSets](5.7-storage-nao-compartilhado-com-statefulsets.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
