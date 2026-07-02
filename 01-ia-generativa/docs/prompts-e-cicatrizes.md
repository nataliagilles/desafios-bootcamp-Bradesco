# 🧠 Engenharia de Prompts e Cicatrizes

Este documento registra os prompts estratégicos testados no NotebookLM ao longo do estudo, o objetivo de cada um, um resumo da resposta obtida e o aprendizado (ou dificuldade) extraído da formulação da pergunta.

Voltar para o [README](../README.md) · Ver o [Miniguia de Estudo](./miniguia-de-estudo.md)

---

### Prompt 1 — Levantamento de princípios
> *"De acordo com essas fontes, quais são as características mais importantes de um código de alta qualidade?"*

**Objetivo:** mapear os princípios fundamentais antes de comparar linguagens.

**Resposta obtida (resumo):** a IA organizou a resposta em 7 categorias — legibilidade e nomes significativos, simplicidade (KISS/YAGNI), ausência de duplicação (DRY), funções pequenas e coesas (SRP/SLAP), testabilidade, refatoração contínua (regra do escoteiro) e documentação integrada (Doc-as-Code).

**Aprendizado:** pedir "de acordo com essas fontes" ancorou a resposta nos documentos carregados, evitando respostas genéricas de conhecimento geral da IA.

---

### Prompt 2 — Comparação entre linguagens
> *"Com base nos arquivos-fonte enviados, compare como C#, Java e Python aplicam esses princípios de qualidade de código."*

**Objetivo:** identificar convenções específicas de cada linguagem.

**Resposta obtida (resumo):** a IA gerou uma tabela comparativa (nomenclatura, documentação, IDE de referência, gestão de dados) e destacou que Python segue PEP 8 (snake_case), Java usa Google Java Style (camelCase + Javadoc) e C# usa PascalCase quase universal + XML comments.

**Aprendizado:** pedir explicitamente "destaque semelhanças e diferenças" produziu uma resposta estruturada em tabela, muito mais útil para consulta rápida do que um texto corrido.

---

### Prompt 3 — Checklist de revisão
> *"Crie uma lista de verificação que possa ser usada durante uma revisão de código."*

**Objetivo:** transformar teoria em uma ferramenta prática de uso diário.

**Resposta obtida (resumo):** checklist em 7 blocos — nomenclatura, design/arquitetura, simplicidade, tratamento de erros, testes (F.I.R.S.T.), documentação e regra do escoteiro.

**Aprendizado:** pedir uma "lista de verificação" (formato de artefato) em vez de "explique" mudou completamente o formato de saída — a IA passou de texto explicativo para itens acionáveis.

---

### Prompt 4 — Análise de código real
> Colei um trecho de código Java (`Calculator`) e pedi: *"Analise este código de acordo com os arquivos-fonte fornecidos. Identifique violações das melhores práticas, explique por que são problemáticas e sugira melhorias."*

**Objetivo:** validar se a IA consegue aplicar a teoria estudada a um caso concreto.

**Resposta obtida (resumo):** identificou 5 violações (nomes não significativos, números mágicos, violação de SRP/OCP, falta de tratamento de erros, formatação) e propôs uma versão refatorada usando `enum` para eliminar a estrutura condicional.

**Aprendizado:** anexar o código real e pedir para justificar cada ponto **com base nas fontes** evitou respostas superficiais do tipo "está tudo errado" e obrigou a IA a explicar o "porquê" de cada problema.

---

### Prompt 5 — Questionando a própria resposta da IA
> *"A análise anterior sugeriu o padrão Strategy. Considerando o princípio KISS, essa recomendação é apropriada para uma calculadora tão pequena? Justifique com base apenas nas fontes."*

**Objetivo:** testar o pensamento crítico da IA e evitar aceitar a primeira resposta como definitiva.

**Resposta obtida (resumo):** a própria IA reconheceu que, para um exemplo tão pequeno, o padrão Strategy é "overkill" segundo Fowler, e que a recomendação só se justifica se o sistema tende a crescer — citando a tensão real entre os princípios YAGNI e OCP.

**Aprendizado (o mais valioso do projeto):** **nem toda recomendação de uma IA é adequada ao contexto**. Reformular a pergunta como um contraponto ("isso não seria exagero?") produziu uma resposta mais honesta e matizada do que a resposta original.

---

## ⚠️ Dificuldades encontradas (cicatrizes)

- Prompts genéricos ("o que é um bom código?") geravam respostas rasas e sem citação às fontes.
- Especificar a linguagem-alvo (Java, C# ou Python) aumentou muito a precisão das respostas.
- Pedir explicitamente "com base nas fontes" reduziu alucinações e respostas fora do escopo do material carregado.
- A primeira resposta da IA nem sempre era a mais adequada — questionar criticamente (Prompt 5) revelou nuances importantes que a resposta inicial tinha ignorado.
- Pedir formatos de saída específicos (tabela, checklist, lista) mudou a utilidade prática da resposta mais do que reformular o conteúdo da pergunta.
