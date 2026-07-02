
# Quality Code

Caderno de estudos sobre qualidade de código, engenharia de software e revisão de código assistida por IA, aplicado a C#, Java e Python. Construído com o apoio do Google NotebookLM como parte do desafio de projeto da Digital Innovation One (DIO).

---

## Contexto e Objetivos

O tema deste caderno é qualidade de código, com foco em três pontos principais: 
- Código Limpo, refatoração e revisão de código.

Também é mostrado como esses conceitos aparecem na prática em três linguagens muito utilizadas no mercado: Java, C# e Python
A escolha do tema partiu de uma necessidade de entender não apenas o que é um código de qualidade, mas por que ele é considerado assim, e como usar uma IA (NotebookLM) como ferramenta de estudo crítico, e não como fonte de respostas prontas.

Objetivos de estudo:
- Compreender os fundamentos de código limpo (Clean Code) e os princípios DRY, KISS, YAGNI e SOLID;
- Estudar como testes automatizados e refatoração se sustentam mutuamente no ciclo de desenvolvimento;
- Entender o que compõe uma documentação de código eficiente além do texto (docstrings, comentários, Doc-as-Code);
- Comparar convenções de nomenclatura, documentação e ferramentas entre Java, C# e Python;
- Aplicar esse conhecimento na análise crítica de um código real;
- Praticar Engenharia de Prompts, testando variações e documentando os resultados;
- Construir um miniguia de estudo reutilizável para revisões futuras.

Ferramentas utilizadas: Google NotebookLM, GitHub, Markdown, Java, C#, Python.

---

## Curadoria de Fontes

Fontes abertas carregadas no NotebookLM para fundamentar as respostas da IA:

| Fonte | Tipo | Link |
|---|---|---|
| PEP 8 – Style Guide for Python Code | Documentação oficial | https://peps.python.org/pep-0008/ |
| Google Java Style Guide | Guia de estilo | https://google.github.io/styleguide/javaguide.html |
| .NET / C# Coding Conventions (Microsoft Learn) | Documentação oficial | https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions |
| Google Engineering Practices (Code Review Guidelines) | Documentação oficial | https://google.github.io/eng-practices/ |

**Referências conceituais complementares** (não carregadas como PDF, usadas como base teórica das respostas):
- *Clean Code* — Robert C. Martin
- *Refactoring* — Martin Fowler

As quatro primeiras fontes foram baixadas em PDF/texto e inseridas diretamente no NotebookLM. Os livros de Martin e Fowler serviram de referência conceitual complementar, citada pela IA nas respostas geradas.
---

## Engenharia de Prompts e Cicatrizes

Cada prompt abaixo documenta a pergunta feita, o objetivo por trás dela, um resumo da resposta obtida e o que funcionou (ou não) na formulação.

### Prompt 1 - Levantamento de princípios
"De acordo com essas fontes, quais são as características mais importantes de um código de alta qualidade?"

Objetivo: mapear os princípios fundamentais antes de comparar linguagens.

Resposta obtida (resumo): a IA organizou a resposta em 7 categorias - legibilidade e nomes significativos, simplicidade (KISS/YAGNI), ausência de duplicação (DRY), funções pequenas e coesas (SRP/SLAP), testabilidade, refatoração contínua (regra do escoteiro) e documentação integrada (Doc-as-Code).

Aprendizado: pedir "de acordo com essas fontes" ancorou a resposta nos documentos carregados, evitando respostas genéricas de conhecimento geral da IA.

### Prompt 2 - Comparação entre linguagens
"Com base nos arquivos-fonte enviados, compare como C#, Java e Python aplicam esses princípios de qualidade de código."

Objetivo: identificar convenções específicas de cada linguagem.

Resposta obtida (resumo): a IA gerou uma tabela comparativa (nomenclatura, documentação, IDE de referência, gestão de dados) e destacou que Python segue PEP 8 (snake_case), Java usa Google Java Style (camelCase + Javadoc) e C# usa PascalCase quase universal + XML comments.

Aprendizado: pedir explicitamente "destaque semelhanças e diferenças" produziu uma resposta estruturada em tabela, muito mais útil para consulta rápida do que um texto corrido.

### Prompt 3 - Checklist de revisão
"Crie uma lista de verificação que possa ser usada durante uma revisão de código."

Objetivo: transformar teoria em uma ferramenta prática de uso diário.

Resposta obtida (resumo): checklist em 7 blocos - nomenclatura, design/arquitetura, simplicidade, tratamento de erros, testes (F.I.R.S.T.), documentação e regra do escoteiro.

Aprendizado: pedir uma "lista de verificação" (formato de artefato) em vez de "explique" mudou completamente o formato de saída - a IA passou de texto explicativo para itens acionáveis.

### Prompt 4 - Análise de código real
Colei um trecho de código Java (Calculator) e pedi: "Analise este código de acordo com os arquivos-fonte fornecidos. Identifique violações das melhores práticas, explique por que são problemáticas e sugira melhorias."

Objetivo: validar se a IA consegue aplicar a teoria estudada a um caso concreto.

Resposta obtida (resumo): identificou 5 violações (nomes não significativos, números mágicos, violação de SRP/OCP, falta de tratamento de erros, formatação) e propôs uma versão refatorada usando enum para eliminar a estrutura condicional.

Aprendizado: anexar o código real e pedir para justificar cada ponto com base nas fontes evitou respostas superficiais do tipo "está tudo errado" e obrigou a IA a explicar o porquê de cada problema.

### Prompt 5 - Questionando a própria resposta da IA
"A análise anterior sugeriu o padrão Strategy. Considerando o princípio KISS, essa recomendação é apropriada para uma calculadora tão pequena? Justifique com base apenas nas fontes."

Objetivo: testar o pensamento crítico da IA e evitar aceitar a primeira resposta como definitiva.

Resposta obtida (resumo): a própria IA reconheceu que, para um exemplo tão pequeno, o padrão Strategy é "overkill" segundo Fowler, e que a recomendação só se justifica se o sistema tende a crescer, citando a tensão real entre os princípios YAGNI e OCP.

Aprendizado (o mais valioso do projeto): nem toda recomendação de uma IA é adequada ao contexto. Reformular a pergunta como um contraponto ("isso não seria exagero?") produziu uma resposta mais honesta e matizada do que a resposta original.

### Dificuldades encontradas (cicatrizes)
- Prompts genéricos ("o que é um bom código?") geravam respostas rasas e sem citação às fontes.
- Especificar a linguagem-alvo (Java, C# ou Python) aumentou muito a precisão das respostas.
- Pedir explicitamente "com base nas fontes" reduziu alucinações e respostas fora do escopo do material carregado.
- A primeira resposta da IA nem sempre era a mais adequada - questionar criticamente (Prompt 5) revelou nuances importantes que a resposta inicial tinha ignorado.
- Pedir formatos de saída específicos (tabela, checklist, lista) mudou a utilidade prática da resposta mais do que reformular o conteúdo da pergunta.

---

## Miniguia de Estudo

### 1. Características de um código de alta qualidade

| Característica | Em poucas palavras |
|---|---|
| Legibilidade e nomes significativos | Nomes revelam intenção; código lido por humanos antes de máquinas |
| Simplicidade (KISS/YAGNI) | Soluções diretas; não implementar o que "pode ser necessário um dia" |
| Ausência de duplicação (DRY) | Cada regra de negócio tem uma única representação no sistema |
| Funções e classes pequenas e coesas (SRP/SLAP) | Uma função, uma responsabilidade, um nível de abstração |
| Testabilidade | Testes como rede de segurança para refatorar com confiança |
| Refatoração contínua | Regra do escoteiro: deixe o código mais limpo do que encontrou |
| Documentação integrada (Doc-as-Code) | Comentários explicam o porquê, não o como |

### 2. Convenções por linguagem

| Característica | Python | Java | C# |
|---|---|---|---|
| Nome de método | snake_case | camelCase | PascalCase |
| Nome de classe | PascalCase | PascalCase | PascalCase |
| Documentação principal | Docstrings (PEP 257) | Javadoc | XML Comments |
| IDE de referência | PyCharm | IntelliJ IDEA | Visual Studio |
| Gestão de dados | Imutabilidade sugerida | Record Classes | Value Types/Structs |

### 3. Code smells mais comuns e como corrigi-los

Duplicação e estrutura:
- Código duplicado: corrigir com Extrair Função / Subir Método
- Função longa: corrigir com Extrair Função / Substituir Função por Comando
- Lista de parâmetros longa: corrigir com Introduzir Objeto de Parâmetros

Design e acoplamento:
- Obsessão por primitivos: corrigir com Substituir Primitivo por Objeto
- Inveja de recursos: corrigir com Mover Função para o módulo correto
- Cirurgia com espingarda: corrigir centralizando a responsabilidade (Mover Função/Campo)
- Mudança divergente: corrigir com Extrair Classe / Separar em Fases

Semântica e qualidade:
- Nome misterioso: corrigir com Renomear Variável / Mudar Declaração de Função
- Argumentos de flag: corrigir criando métodos explícitos por comportamento
- Dados globais: corrigir com Encapsular Variável
- Comentário como "desodorante": corrigir refatorando até o código ficar autoexplicativo

Era da IA:
- Código espaguete / ifs infinitos gerados por IA: corrigir com Strategy Pattern ou Substituir Condicional por Polimorfismo, mas avaliando antes com o princípio KISS, pois nem sempre vale a complexidade extra (ver item 5).

### 4. Checklist para Code Review

Nomenclatura:
- Os nomes revelam intenção (não exigem comentário para serem entendidos)?
- Seguem a convenção da linguagem (verbo para método, substantivo para classe)?

Design:
- Cada função/classe tem uma única responsabilidade (SRP)?
- Existe lógica duplicada que poderia ser unificada (DRY)?
- O acoplamento está baixo e a coesão alta?

Simplicidade:
- A solução é a mais simples possível para o problema (KISS)?
- Há código implementado "para o futuro" sem necessidade real (YAGNI)?
- Existem números mágicos que deveriam ser constantes nomeadas?

Erros e segurança:
- Pré-condições e casos de borda são validados?
- Exceções são usadas para casos realmente excepcionais?
- Não há segredos expostos nem entradas sem validação (OWASP)?

Testes:
- Existem testes automatizados e eles passam?
- Os testes seguem F.I.R.S.T. (rápidos, independentes, repetíveis, autovalidáveis, oportunos)?

Documentação:
- Comentários explicam o porquê, não o como?
- README/docstrings estão atualizados?
- Não há código morto/comentado poluindo o arquivo?

### 5. Estudo de caso: refatoração de uma calculadora Java

Código original analisado (nomes genéricos, números mágicos, sem tratamento de erros):

```java
public class Calculator {
    public int calc(int a, int b, int op) {
        if (op == 1) return a + b;
        if (op == 2) return a - b;
        if (op == 3) return a * b;
        if (op == 4) return a / b;
        return 0;
    }
}
```

Versão refatorada com nomes significativos, enum no lugar de números mágicos e tratamento explícito de erro:

```java
public class Calculator {
    public enum Operation {
        ADDITION { public int apply(int a, int b) { return a + b; } },
        SUBTRACTION { public int apply(int a, int b) { return a - b; } },
        MULTIPLICATION { public int apply(int a, int b) { return a * b; } },
        DIVISION {
            public int apply(int a, int b) {
                if (b == 0) throw new IllegalArgumentException("Divisor cannot be zero.");
                return a / b;
            }
        };

        public abstract int apply(int a, int b);
    }

    public int calculate(int firstNumber, int secondNumber, Operation operation) {
        if (operation == null) {
            throw new IllegalArgumentException("Operation cannot be null.");
        }
        return operation.apply(firstNumber, secondNumber);
    }
}
```

Ressalva importante: para este exemplo específico (4 operações fixas), essa refatoração com enum já resolve o essencial. Um padrão Strategy completo, com classes separadas por operação, só se justifica se o sistema for crescer para dezenas de operações; caso contrário, fere o princípio KISS (ver Prompt 5, na seção de Engenharia de Prompts).

### 6. Glossário

| Termo | Definição |
|---|---|
| Clean Code | Código legível, simples e fácil de manter, priorizando a compreensão humana |
| DRY (Don't Repeat Yourself) | Cada regra de negócio deve ter uma única representação no sistema |
| KISS (Keep It Simple, Stupid) | Priorizar soluções simples em vez de arquiteturas complexas |
| YAGNI (You Ain't Gonna Need It) | Não implementar funcionalidades baseadas em suposições futuras |
| SOLID | Conjunto de 5 princípios de design orientado a objetos (SRP, OCP, LSP, ISP, DIP) |
| SRP (Single Responsibility Principle) | Cada módulo/classe/função deve ter apenas um motivo para mudar |
| OCP (Open/Closed Principle) | Código aberto para extensão, fechado para modificação |
| SLAP (Single Level of Abstraction Principle) | Todas as instruções de uma função devem estar no mesmo nível de detalhe |
| Code Smell | Indicador superficial de que o design pode precisar de refatoração |
| Refactoring | Melhorar a estrutura interna do código sem alterar seu comportamento observável |
| Regra do Escoteiro | Deixar o código mais limpo do que se encontrou |
| Technical Debt | Custo futuro de manutenção gerado por decisões de implementação inadequadas |
| F.I.R.S.T. | Princípios de testes de qualidade: Fast, Independent, Repeatable, Self-validating, Timely |
| TDD | Test-Driven Development, escrever o teste antes do código funcional |
| Doc-as-Code | Tratar a documentação como parte do código, versionada e sempre atualizada |

### 7. Prompts reutilizáveis

```
Com base nas fontes carregadas, quais são as características mais importantes de um código de alta qualidade em [linguagem]?
```

```
Compare como [linguagem A] e [linguagem B] aplicam os princípios DRY, KISS e SOLID, destacando semelhanças e diferenças específicas de cada uma.
```

```
Crie uma checklist de code review baseada nas fontes fornecidas, organizada por categorias (nomenclatura, design, testes, erros, documentação).
```

```
Analise este código [colar código] de acordo com as fontes fornecidas. Identifique violações de boas práticas, explique por que são problemáticas e sugira melhorias.
```

```
A sugestão anterior é realmente necessária para este caso, ou seria "overkill" considerando o princípio KISS? Justifique com base apenas nas fontes.
```

```
Quais code smells esse trecho de código apresenta e qual refatoração específica (nome da técnica) resolveria cada um?
```

---

## Principal aprendizado

Escrever código funcional não é suficiente: código de qualidade precisa ser legível, simples, testável e preparado para evoluir. O uso do NotebookLM como ferramenta de estudo mostrou que a IA é mais útil quando usada para provocar pensamento crítico do que para gerar respostas definitivas. Questionar a própria recomendação da IA (Prompt 5) foi o experimento mais valioso do projeto, porque revelou que a IA reconsidera e refina suas respostas quando desafiada com o contexto certo.

---




## Material de estudo Separado
- **[📄 Engenharia de Prompts e Cicatrizes](./docs/prompts-e-cicatrizes.md)** — 5 prompts testados no NotebookLM, com o objetivo de cada um, um resumo das respostas e o que foi aprendido em cada tentativa sobre como fazer boas perguntas.
- **[📄 Miniguia de Estudo](./docs/miniguia-de-estudo.md)** — versão final do material, com resumos organizados por tema, uma tabela comparando linguagens, checklist de revisão de código, um caso prático de refatoração de uma calculadora em Java e um glossário completo.

---


## Autora


Natália Rodrigues Gilles

Desenvolvido como parte do desafio de projeto da Digital Innovation One (DIO), utilizando o Google NotebookLM.
