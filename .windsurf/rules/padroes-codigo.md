---
trigger: always_on
description: 
globs: 
---

## Grupo 1 — Clean Code e Boas Práticas Gerais

| Nº    | Regra                                                                                                                                                                 |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R1.1  | Todo o código-fonte **deve ser escrito em inglês**, incluindo nomes de variáveis, classes, métodos e comentários.                                                     |
| R1.2  | **Aplicar os princípios de Clean Code**, observando as recomendações complementares descritas neste guia.                                                             |
| R1.3  | **Utilizar**: camelCase para métodos, funções e variáveis; PascalCase para classes e interfaces; e kebab-case para arquivos e diretórios.                             |
| R1.4  | **Nomear métodos e funções com verbos** que expressem claramente a ação executada. O nome deve refletir um único propósito e não deve começar com substantivo.        |
| R1.5  | **Evitar efeitos colaterais**. Cada método ou função deve ter um único propósito e não deve alterar o estado de forma implícita.                                      |
| R1.6  | **Evitar parâmetros do tipo flag** (booleanos ou equivalentes) que alterem o comportamento de métodos. Extraia comportamentos distintos em métodos separados.         |
| R1.7  | **Evitar aninhamentos superiores a dois níveis** de `if/else`. Prefira **early return** para simplificar a leitura.                                                   |
| R1.8  | **Limitar métodos a até três parâmetros**. Quando ultrapassar esse número, utilize objetos para encapsular dados relacionados.                                        |
| R1.9  | **Manter métodos curtos**, com no máximo 30 linhas. O ideal é entre 10 e 15 linhas, priorizando legibilidade.                                                         |
| R1.10 | **Evitar classes extensas**, com limite máximo de 300 linhas. Sempre que possível, divida em componentes menores e coesos.                                            |
| R1.11 | **Substituir magic numbers por constantes nomeadas**. As constantes devem ter nomes descritivos que representem claramente o significado e o contexto do valor.       |
| R1.12 | **Definir mensagens de exceção como constantes nomeadas**. Os nomes devem refletir o propósito e o contexto da mensagem.                                              |
| R1.13 | **Evitar abreviações** e nomes excessivamente longos (mais de 30 caracteres). Buscar equilíbrio entre clareza e concisão.                                             |
| R1.14 | **Evitar comentários desnecessários**. O código deve ser autoexplicativo. Use comentários apenas para justificar decisões técnicas relevantes.                        |
| R1.15 | **Declarar apenas uma variável por linha** para aumentar a legibilidade e facilitar a depuração.                                                                      |
| R1.16 | **Declarar variáveis por inferência de tipo** (usando `var`) quando o tipo puder ser claramente deduzido pelo compilador.                                             |
| R1.17 | **Declarar variáveis próximas ao ponto de uso**, para reduzir escopo e aumentar a clareza.                                                                            |
| R1.18 | **Evitar linhas em branco desnecessárias** dentro de métodos e funções. Mantenha apenas o espaçamento que favoreça a leitura lógica.                                  |
| R1.19 | **Não utilizar espaçamento duplo** entre blocos de código. Uma linha em branco é suficiente para separar trechos lógicos.                                             |
| R1.20 | **Evitar criar o construtor de uma classe com parâmetro por linha** utilize o máximo de parâmetros por linha, respeitando o total de 120 colunas.                     |
| R1.21 | **A estrutura 'if' deve utilizar '{}'s.** utilize a estrura condicional if com parênteses '()' para definir a condição e chaves '{}' para encapsular o comportamento. |

## Grupo 2 — Design e Arquitetura

| Nº   | Regra                                                                                                                                                                          |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| R2.1 | **Aplicar o Princípio da Inversão de Dependência (DIP)** em controllers, use cases, services e adaptadores. Recursos externos devem depender de abstrações, nunca o contrário. |
| R2.2 | **Preferir composição a herança**, privilegiando flexibilidade e baixo acoplamento entre classes.                                                                              |
| R2.3 | **Utilizar Spring Data JPA** para operações de persistência, adotando o serviço mais apropriado ao modelo de domínio.                                                          |

## Grupo 3 — Check Style e Code Style

| Nº   | Regra                                                                                                                               |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------- |
| R3.1 | **Aplicar as regras de formatação e validação de código definidas em `@checkstyle.xml`.**                                           |
| R3.2 | **Seguir as convenções de estilo definidas em `@codestyle.xml`,** garantindo consistência em todo o projeto.                        |
| R3.3 | No front-end, seguir rigorosamente os padrões definidos pelo ESLint e Prettier para garantir consistência e padronização do código. |
