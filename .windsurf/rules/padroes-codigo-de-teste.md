---
trigger: model_decision
description: 
globs: 
---

## Como aplicar (design recomendado)

Para **criar testes de unidade** de forma consistente e alinhada a este padrão, utilize a skill:

- `.windsurf/skills/skill-generate-unit-tests/SKILL.md`

Esta rule permanece como a **referência normativa** (regras e exemplos). A skill define o **processo** para gerar os testes seguindo estas regras.

## Grupo 1 — Configuração e Estrutura

| Nº  | Regra                                                                                                                                                                                 |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R1.1  | **Utilizar JUnit 5** para definir cenários de teste, **Mockito** para implementar padrões de teste (_stub_, _spy_ e _mock_), e **AssertJ** para expressar asserções fluentes.         |
| R1.2  | **Organizar os testes** no diretório `src/test/java`, mantendo-os próximos às classes testadas. Cada classe de teste deve terminar com o sufixo `Test` (ex.: `UserServiceTest.java`). |
| R1.3  | **Nomear os métodos de teste em inglês**, descrevendo a ação e o resultado esperado (ex.: `shouldReturnUserWhenEmailIsValid`).                                                        |

## Grupo 2 — Boas Práticas de Teste

| Nº  | Regra                                                                                                                                                                   |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R2.1 | **Aplicar os princípios do FIRST** nos testes. |
| R2.2  | **Evitar dependências entre testes.** Cada teste deve ser independente, determinístico e idempotente.                                                                   |
| R2.3  | **Seguir o padrão Arrange, Act, Assert (ou Given, When, Then)** para estruturar os testes. |
| R2.4 | **Não inserir linhas em branco** dentro das seções *Arrange*, *Act* ou *Assert*. |
| R2.5 | **Inserir linhas em branco** para separar as seções *Arrange*, *Act* ou *Assert*. |
| R2.5 | **Testar um único comportamento por teste.** Evitar testes longos e preferir vários testes pequenos e específicos.                                                      |
| R2.6 | **Garantir que o código seja testável.** Evitar estados globais, _singletons_ e métodos estáticos difíceis de isolar. Priorizar injeção de dependências.                |
| R2.7 | **Evitar verificações redundantes com Mockito.** Não utilizar `verify()` quando o comportamento já estiver garantido por configuração de _mock_.                        |
| R2.8 | **Aplicar os princípios de Clean Code** também nos testes, mantendo clareza, simplicidade e consistência.                                                               |

## Grupo 3 — Testes de Unidade e Integração

| Nº  | Regra                                                                                                                                                                 |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R3.1 | **Criar testes unidade** para validar as menores partes do código. |
| R3.2 | **Classificar como teste de integração** qualquer teste que dependa de HTTP, banco de dados, mensageria, sistema de arquivos ou APIs externas.                        |
| R3.3 | **Utilizar as anotações `@IntegrationTest` e `@AutoConfigureMockMvc`** para configurar testes de integração.                                                          |
| R3.4 | **Usar a classe `SecurityMfaApiTest` como referência** para a estrutura e práticas recomendadas de testes de integração.                                              |
| R3.5 | **Criar testes integração** para o fluxo principal do sistema, validando *status codes*, *payloads* e mensagens de erro. |
| R3.6 | **Implementar teste de autenticação** que valide o acesso de usuários a endpoints protegidos (ex.: `shouldReturnUnauthorizedWhenRequestToMfaUrisIsNotAuthenticated`). |
| R3.7 | **Reservar a validação de regras de negócio complexas** para testes de unidade nos _use cases_ e _services_.                                                          |
| R3.8 | **Garantir cobertura de testes** para todos os _services_, validators, abrangendo fluxos principais e alternativos (incluindo _exceptions_).                        |
| R3.9 | **Utilizar stubs ou mocks** para evitar chamadas a APIs externas e bancos de dados em testes de unidade.                                                              |
| R3.10 | **Inverter dependências via interfaces e injetar colaborações por construtor**, facilitando o uso de _stubs_ e _mocks_ durante os testes.                             |

## Grupo 4 — Recursos e Ferramentas

| Nº  | Regra                                                                                                                                                                                           |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R4.1 | **Utilizar AssertJ** para criar asserções fluentes e legíveis. |
| R4.2 | **Verificar interações relevantes** com Mockito (`verify(...)`) apenas quando necessário. |
| R4.3 | **Encerrar recursos e conexões manualmente** em `@AfterEach` / `@AfterAll`. Em ambientes com Spring + Testcontainers, preferir o ciclo de vida controlado com `@Testcontainers` e `@Container`.|
| R4.4 | **Usar `@BeforeEach` para inicialização leve e determinística**, evitando lógica complexa nessa etapa. |

## Grupo 5 — Clean Code e Padrões Gerais

| Nº  | Regra                                                                                                                     |
| --- | ------------------------------------------------------------------------------------------------------------------------- |
| R5.1 | **Evitar o uso de magic numbers.** Substituí-los por constantes nomeadas que descrevam o propósito do valor. |
| R5.2 | **Definir mensagens de exceção como constantes nomeadas.** O nome deve refletir o contexto e o propósito da mensagem. |
| R5.3 | **Declarar variáveis utilizando inferência de tipo (`var`)** quando o tipo puder ser claramente deduzido pelo compilador. |
| R5.4 | **Constantes** aproveite as constantes públicas declaradas nas classes de constantes nos testes. |

## Exemplos rápidos

### 1) Teste de unidade com Mockito e AssertJ

Exemplo alinhado ao que a skill `skill-generate-unit-tests` deve produzir (ajuste nomes e cenários conforme o seu caso).

```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {

  @Mock
  private UserRepository userRepository;
  @InjectMocks
  private UserService userService;

  @Test
  void shouldReturnUserWhenEmailIsValid() {
    var email = "john.doe@company.com";
    var user = new User("1", email);
    when(userRepository.findByEmail(email)).thenReturn(Optional.of(user));

    var result = userService.findByEmail(email);

    assertThat(result).isPresent().contains(user);
    verifyNoMoreInteractions(userRepository);
  }
}
```