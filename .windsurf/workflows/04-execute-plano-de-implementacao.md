---
description: 
---
 # 4. Executar o plano de implementação
 
 <critical>
   Este workflow deve consumir os artefatos gerados pelas skills registradas:
   - PRD: `skill-generate-prd` em `.windsurf/skills/skill-generate-prd/SKILL.md`
   - Tech Spec: `skill-generate-techspec` em `.windsurf/skills/skill-generate-techspec/SKILL.md`
   - Task Plan: `skill-generate-task-plan` em `.windsurf/skills/skill-generate-task-plan/SKILL.md`
 </critical>

## Inputs

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="TASK_PLAN_NAME">
  Nome do arquivo do Task Plan a ser lido (gerado no passo 03).
</instrucao>

 Com base no Task Plan informado, inicie a execução da implementação do código. Se precisar de mais contexto, leia o PRD e a Tech Spec relacionados.

## Instruções:

- Obtenha o contexto da tarefa lendo o arquivo que contém o plano de implementação através do <TASK_PLAN_NAME> que é o nome do arquivo que foi digitado após a instrução /04-execute-plano-de-implementacao.md <MICROSSERVICO> <TASK_PLAN_NAME>. Se precisar de mais contexto, leia o PRD e a Tech Spec relacionados.
- Identifique o plano a ser implementado se o comando '04-execute-plano-de-implementacao <MICROSSERVICO>' for seguido do número do plano, por exemplo 1 ou 01, 2 ou 02, 3 ou 03 e assim por diante, que foi definido no workflow '03-avalie-divisao-plano-de-implementacao-criar-tarefas'. 
- Para cada etapa do plano, descreva sucintamente a ação de desenvolvimento a ser realizada.
- Para cada etapa finalizada, valide se está aderente ao objetivo da tarefa e critérios de aceite.
- Se necessário, registre bloqueios, decisões técnicas ou desvios.
- Aplique as regras na rule @padroes-codigo.md.
- Aplique as regras de design de software contidas rule @geracao-classes-architecture.md, se for necessário criar/alterar pacotes
- Aplique as regras de teste contidas na rule @padroes-codigo-de-teste.md, se estiver implementando testes
- Ao final da implementação, execute os testes de unidade e de integração. Caso algum teste falhe, analise a falha e implemente a correção.
  - Para a execução dos testes, utilize o Java da máquina. Se não encontrar, pesquise se o Java foi instalado pelo SDKMAN (export JAVA_HOME=~/.sdkman/candidates/java/current).
  - Para a execução dos testes de unidade, utilize gradlew test
  # - Para a execução dos testes de integração, utilize gradlew integrationTest

Formato de acompanhamento (para relatório):

Execução da Implementação - <DATA-ATUAL>
Etapa 1: [Descrição]

Ação realizada: [...]

Observações: [...]

Etapa 2: [Descrição]

Ação realizada: [...]

Observações: [...]

...

Observações Finais

[Inclua possíveis desvios do plano, problemas encontrados, pendências]

Use linguagem técnica objetiva. Não inclua código-fonte aqui.

Importante: Não invente informações.