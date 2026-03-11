---
name: skill-generate-unit-tests
description: Gerar testes de unidade (JUnit 5 + Mockito + AssertJ) seguindo padrões do projeto
---

# Skill - Gerar Testes de Unidade

<critical>
  Gere testes de unidade usando JUnit 5, Mockito e AssertJ.
  Siga as regras de estrutura e estilo definidas em `.windsurf/rules/padroes-codigo-de-teste.md`.
  Não invente informações: se faltar contexto (classes, contratos, regras), peça ou explicite as suposições.
</critical>

## Entradas

<instrucao id="TARGET_CLASS_FILE">
  Caminho do arquivo da classe a ser testada (ex.: `/microservices/device-management/src/main/java/.../UserService.java`).
</instrucao>

<instrucao id="TARGET_BEHAVIOR">
  Comportamento a ser testado, descrito em uma frase objetiva (ex.: `findByEmail should return user when email exists`).
</instrucao>

<instrucao id="DEPENDENCIES_TO_MOCK">
  Lista de dependências/colaborações que devem ser mockadas (ex.: `UserRepository`, `Clock`). Se não souber, identifique a partir do construtor/campos injetados.
</instrucao>

## Saída

<instrucao id="TEST_CLASS_FILE">
  Caminho do arquivo de teste a ser criado em `src/test/java` (espelhando o package da classe testada) e com sufixo `Test`.
</instrucao>

## Processo

1) Levantar contexto mínimo
- Ler `TARGET_CLASS_FILE`.
- Identificar responsabilidades, dependências (injeção por construtor), exceções e retornos.
- Confirmar o `TARGET_BEHAVIOR` e quais variações relevantes existem (happy path e 1-2 edge cases).

2) Definir a estrutura do teste
- Criar classe `*Test` com JUnit 5.
- Usar `@ExtendWith(MockitoExtension.class)`.
- Declarar `@Mock` para as dependências e `@InjectMocks` para a classe testada.

3) Escrever testes seguindo AAA/GWT
- Organizar o método em seções Arrange, Act, Assert (ou Given, When, Then).
- Não inserir linhas em branco dentro de uma seção.
- Inserir uma linha em branco apenas entre seções.

4) Nomeação e clareza
- Nomear métodos de teste em inglês, com verbo, no formato `should...When...`.
- Testar um único comportamento por teste.

5) Asserções e verificações
- Usar AssertJ para asserções.
- Usar Mockito para stubs (`when(...).thenReturn(...)`).
- Evitar `verify(...)` redundante.
- Quando apropriado, usar `verifyNoMoreInteractions(...)` para assegurar ausência de efeitos colaterais.

## Checklist de validação
- O teste compila (imports e packages corretos).
- O teste é determinístico e independente.
- O teste cobre o comportamento descrito em `TARGET_BEHAVIOR`.
- O teste não depende de HTTP, banco, mensageria, filesystem ou API externa (senão é integração).
