# 🧩 Miniguia de Estudo — Qualidade de Código

Entrega final consolidada do caderno de estudos: resumos estruturados, checklist prática, estudo de caso, glossário e prompts reutilizáveis para revisões futuras.

Voltar para o [README](../README.md) · Ver [Engenharia de Prompts e Cicatrizes](./prompts-e-cicatrizes.md)

---

## 1. Características de um código de alta qualidade

| Característica | Em poucas palavras |
|---|---|
| Legibilidade e nomes significativos | Nomes revelam intenção; código lido por humanos antes de máquinas |
| Simplicidade (KISS/YAGNI) | Soluções diretas; não implementar o que "pode ser necessário um dia" |
| Ausência de duplicação (DRY) | Cada regra de negócio tem uma única representação no sistema |
| Funções e classes pequenas e coesas (SRP/SLAP) | Uma função, uma responsabilidade, um nível de abstração |
| Testabilidade | Testes como rede de segurança para refatorar com confiança |
| Refatoração contínua | Regra do escoteiro: deixe o código mais limpo do que encontrou |
| Documentação integrada (Doc-as-Code) | Comentários explicam o "porquê", não o "como" |

## 2. Convenções por linguagem

| Característica | Python | Java | C# |
|---|---|---|---|
| Nome de método | snake_case | camelCase | PascalCase |
| Nome de classe | PascalCase | PascalCase | PascalCase |
| Documentação principal | Docstrings (PEP 257) | Javadoc | XML Comments |
| IDE de referência | PyCharm | IntelliJ IDEA | Visual Studio |
| Gestão de dados | Imutabilidade sugerida | Record Classes | Value Types/Structs |

## 3. Code smells mais comuns e como corrigi-los

**Duplicação e estrutura**
- *Código duplicado* → Extrair Função / Subir Método
- *Função longa* → Extrair Função / Substituir Função por Comando
- *Lista de parâmetros longa* → Introduzir Objeto de Parâmetros

**Design e acoplamento**
- *Obsessão por primitivos* → Substituir Primitivo por Objeto
- *Inveja de recursos* → Mover Função para o módulo correto
- *Cirurgia com espingarda* → Centralizar responsabilidade (Mover Função/Campo)
- *Mudança divergente* → Extrair Classe / Separar em Fases

**Semântica e qualidade**
- *Nome misterioso* → Renomear Variável / Mudar Declaração de Função
- *Argumentos de flag* → Criar métodos explícitos por comportamento
- *Dados globais* → Encapsular Variável
- *Comentário como "desodorante"* → Refatorar até o código ficar autoexplicativo

**Era da IA**
- *Código espaguete / ifs infinitos gerados por IA* → Strategy Pattern ou Substituir Condicional por Polimorfismo (**mas avalie com KISS antes** — nem sempre vale a complexidade extra, ver seção 5)

## 4. Checklist para Code Review

**Nomenclatura**
- [ ] Os nomes revelam intenção (não exigem comentário para serem entendidos)?
- [ ] Seguem a convenção da linguagem (verbo para método, substantivo para classe)?

**Design**
- [ ] Cada função/classe tem uma única responsabilidade (SRP)?
- [ ] Existe lógica duplicada que poderia ser unificada (DRY)?
- [ ] O acoplamento está baixo e a coesão alta?

**Simplicidade**
- [ ] A solução é a mais simples possível para o problema (KISS)?
- [ ] Há código implementado "para o futuro" sem necessidade real (YAGNI)?
- [ ] Existem números mágicos que deveriam ser constantes nomeadas?

**Erros e segurança**
- [ ] Pré-condições e casos de borda são validados?
- [ ] Exceções são usadas para casos realmente excepcionais?
- [ ] Não há segredos expostos nem entradas sem validação (OWASP)?

**Testes**
- [ ] Existem testes automatizados e eles passam?
- [ ] Os testes seguem F.I.R.S.T. (rápidos, independentes, repetíveis, autovalidáveis, oportunos)?

**Documentação**
- [ ] Comentários explicam o "porquê", não o "como"?
- [ ] README/docstrings estão atualizados?
- [ ] Não há código morto/comentado "poluindo" o arquivo?

## 5. Estudo de caso: refatoração de uma calculadora Java

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

Versão refatorada com nomes significativos, `enum` no lugar de números mágicos e tratamento explícito de erro:

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

> **Ressalva importante:** para este exemplo específico (4 operações fixas), essa refatoração com `enum` já resolve o essencial. Um padrão `Strategy` completo, com classes separadas por operação, só se justifica se o sistema for crescer para dezenas de operações — caso contrário, fere o princípio KISS (ver detalhes em [prompts-e-cicatrizes.md](./prompts-e-cicatrizes.md#prompt-5--questionando-a-própria-resposta-da-ia)).

## 6. Glossário

| Termo | Definição |
|---|---|
| **Clean Code** | Código legível, simples e fácil de manter, priorizando a compreensão humana |
| **DRY** (Don't Repeat Yourself) | Cada regra de negócio deve ter uma única representação no sistema |
| **KISS** (Keep It Simple, Stupid) | Priorizar soluções simples em vez de arquiteturas complexas |
| **YAGNI** (You Ain't Gonna Need It) | Não implementar funcionalidades baseadas em suposições futuras |
| **SOLID** | Conjunto de 5 princípios de design orientado a objetos (SRP, OCP, LSP, ISP, DIP) |
| **SRP** (Single Responsibility Principle) | Cada módulo/classe/função deve ter apenas um motivo para mudar |
| **OCP** (Open/Closed Principle) | Código aberto para extensão, fechado para modificação |
| **SLAP** (Single Level of Abstraction Principle) | Todas as instruções de uma função devem estar no mesmo nível de detalhe |
| **Code Smell** | Indicador superficial de que o design pode precisar de refatoração |
| **Refactoring** | Melhorar a estrutura interna do código sem alterar seu comportamento observável |
| **Regra do Escoteiro** | Deixar o código mais limpo do que se encontrou |
| **Technical Debt** | Custo futuro de manutenção gerado por decisões de implementação inadequadas |
| **F.I.R.S.T.** | Princípios de testes de qualidade: Fast, Independent, Repeatable, Self-validating, Timely |
| **TDD** | Test-Driven Development — escrever o teste antes do código funcional |
| **Doc-as-Code** | Tratar a documentação como parte do código, versionada e sempre atualizada |

## 7. Prompts reutilizáveis

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
