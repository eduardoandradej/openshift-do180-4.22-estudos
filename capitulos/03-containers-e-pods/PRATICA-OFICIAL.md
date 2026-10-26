# Prática oficial — Capítulo 3

> Ponte para as atividades do curso. **Não** reproduz enunciados, passos, respostas
> ou soluções. Execute tudo no ambiente oficial, no `workstation`, como `student`.
> As credenciais estão no enunciado de cada atividade.

## Visão geral

| Seção | Tipo | Identificador `lab` | `lab grade` | PDF |
|-------|------|---------------------|-------------|-----|
| 3.2 | Guided Exercise | `pods-containers` | Não | p. 169–176 |
| 3.4 | Guided Exercise | `pods-images` | Não | p. 190–200 |
| 3.6 | Guided Exercise | `pods-troubleshooting` | Não | p. 208–213 |
| 3.7 | Lab | `pods-review` | **Sim** | p. 214–221 |
| 3.8 | Quiz | — (usa `skopeo` e `oc image` contra o registry da sala) | — | p. 222–225 |

Identificadores e avaliação verificados no PDF do Capítulo 3.

---

## 3.2 Guided Exercise: Create Linux Containers and Kubernetes Pods

| Campo | Valor |
|-------|-------|
| Seção | 3.2 |
| Identificador `lab` | `pods-containers` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 169–176 |

**Competência praticada:** criar um Pod com um container e localizá-lo no runtime
do nó; ver logs; ler, de dentro do container, a versão do SO e os processos;
identificar PID e namespaces do container; ler as faixas de UID/GID do projeto;
comparar namespaces entre Pods; entender a função de cada container em um Pod com
vários containers.

**Domine antes:** [3.1](3.1-criar-containers-e-pods.md), especialmente `oc run`,
`restartPolicy`, faixas de UID e o roteiro `crictl` → PID → `lsns`/`nsenter`.

```bash
lab start pods-containers
lab finish pods-containers
```

**Pontos de atenção:**
- Para comandos pontuais, lembre da política de reinício adequada.
- O acesso ao nó (`oc debug node/...`) exige o usuário administrador.
- Compare o **UID** visto dentro do container com a faixa do projeto.
- Ao comparar Pods, observe quais namespaces são diferentes e quais são compartilhados.

---

## 3.4 Guided Exercise: Find and Inspect Container Images

| Campo | Valor |
|-------|-------|
| Seção | 3.4 |
| Identificador `lab` | `pods-images` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 190–200 |

**Competência praticada:** usar uma imagem MySQL suportada para rodar Pods de
servidor e de cliente; testar imagens de comunidade e comparar seus requisitos de
execução; inspecionar imagens remotas e logs; definir variáveis de ambiente e
substituir o comando de entrada; acessar arquivos dentro do container.

**Domine antes:** [3.3](3.3-encontrar-e-inspecionar-imagens.md) (skopeo,
`oc image info`, `USER`, root × não root) e [3.1](3.1-criar-containers-e-pods.md)
(`--env`, `--command`).

```bash
lab start pods-images
lab finish pods-images
```

**Pontos de atenção:**
- Antes de rodar uma imagem, **inspecione** usuário, variáveis e comando.
- Quando uma imagem de comunidade falhar, use logs, um debug pod e as permissões de diretórios para descobrir **por quê**, e relacione com a política de UIDs do OpenShift.
- Imagens podem exigir variáveis obrigatórias para iniciar.

---

## 3.6 Guided Exercise: Troubleshoot Containers and Pods

| Campo | Valor |
|-------|-------|
| Seção | 3.6 |
| Identificador `lab` | `pods-troubleshooting` |
| Avaliação | Sem `lab grade` |
| Referência | PDF p. 208–213 |

**Competência praticada:** investigar a falha na criação de um Pod MySQL; ver
status, logs e eventos; checar no registry quais manifestos existem; copiar
arquivos para o Pod; conectar-se por port forwarding e inicializar dados de teste.

**Domine antes:** [3.5](3.5-diagnosticar-containers-e-pods.md) inteira, em especial
a tabela de estados de falha e o roteiro da Parte B.

```bash
lab start pods-troubleshooting
lab finish pods-troubleshooting
```

**Pontos de atenção:**
- O status do Pod indica **em que etapa** a falha ocorre; comece por ele.
- O `skopeo` precisa de login no registry da sala antes de inspecionar.
- O `oc port-forward` ocupa o terminal: use um segundo terminal para os testes.

---

## 3.7 Lab: Run Applications as Containers and Pods

| Campo | Valor |
|-------|-------|
| Seção | 3.7 |
| Identificador `lab` | `pods-review` |
| Avaliação | **`lab grade pods-review`** |
| Referência | PDF p. 214–221 |

**Competência praticada (resumo autoral):** implantar um Pod de servidor web a
partir de uma imagem; obter status e eventos; diagnosticar a falha com um debug
pod; editar o Pod para usar uma versão corrigida da imagem; confirmar que o
usuário do container é não privilegiado e pertence ao grupo root, com permissões
corretas de diretório; conectar-se por port forwarding; copiar um arquivo de
diagnóstico para o Pod e verificá-lo pelo navegador.

**Domine antes:** as três lições e a [revisão](REVISAO.md).

```bash
lab start pods-review
lab grade pods-review       # com o port-forward ainda ativo em outro terminal
lab finish pods-review
```

**Pontos de atenção:**
- O enunciado pede que o **port-forward continue ativo** durante o `lab grade`; só depois encerre com Ctrl+C.
- Trocar a imagem de um Pod é uma das poucas mudanças permitidas em um Pod existente.
- Verifique UID, GID e permissões do diretório indicado **depois** da troca de imagem.

---

## 3.8 Quiz: Run Applications as Containers and Pods

| Campo | Valor |
|-------|-------|
| Seção | 3.8 |
| Tipo | Quiz prático |
| Referência | PDF p. 222–225 |

As questões pedem dados reais de imagens do registry da sala: comando executado,
UID e consequências no OpenShift, hash de uma tag, variáveis de ambiente, tags
disponíveis e quais imagens rodam com determinado usuário. Faça login no registry
com `skopeo` e responda com `skopeo inspect [--config]`, `skopeo list-tags` e `oc
image info`. As respostas não são registradas aqui.

---

**Registro:** anote cada atividade no [diário de laboratórios](../../progresso/diario-de-laboratorios.md).

---
[← 3.5 Diagnóstico](3.5-diagnosticar-containers-e-pods.md) | [Índice do capítulo](README.md) | [Próximo: Revisão →](REVISAO.md)
