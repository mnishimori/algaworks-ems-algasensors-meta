---
description: 
---

## 3. Avaliar necessidade de divisão do plano em MRs e tarefas menores

Utilize o arquivo de PRD prompt (workflow) para obter o contexto da tarefa após o nome deste arquivo ser mencionado.

Obtenha o código da tarefa do nome do arquivo que foi digitado após a instrução /03-avalie-divisao-plano-de-implementacao-criar-tarefas.md <MICROSSERVICO> <TECHSPEC_NAME>.

<critical>
  Este workflow deve delegar a geração do Task Plan para a skill registrada `skill-generate-task-plan`.
  Referência: `.windsurf/skills/skill-generate-task-plan/SKILL.md`.
</critical>

<critical>
  Após obtido o contexto da tarefa, crie um arquivo de task plan, conforme instruções contidas neste arquivo.
  Não realize nenhuma implementação.
</critical>

## Inputs

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="TECHSPEC_NAME">
  Nome do arquivo da Tech Spec a ser lida (gerada no passo 02).
</instrucao>

## Fluxo de Trabalho

Com base na Tech Spec informada (e, se necessário, lendo o PRD relacionado), avalie se é necessário dividir a implementação em múltiplos Merge Requests e/ou tarefas.
Salve o resultado em um relatório no formato Markdown conforme regras definidas na skill registrada `skill-generate-task-plan`.

### Critérios para divisão:
- Complexidade elevada ou alto risco técnico
- Componentes independentes ou paralelizáveis
- Facilitar code review e teste incremental
- Reduzir riscos de regressão
- Otimizar processo de validação com o time de QA ou Produto

---

### Saída esperada:

Avaliação de Divisão - <DATA-ATUAL>
Justificativa para divisão
[Sim ou Não + motivo técnico claro]

Sugestão de Divisão
Tarefa 1: [Nome objetivo]
MR 1: [Escopo principal desta entrega]

Tarefa 2: [Nome objetivo]
MR 2: [Escopo principal desta entrega]

...
Considerações
[Impactos no planejamento, comunicação necessária, dependências entre tarefas/MRs]
---

<critical>Não invente informações. Se algo estiver ausente no contexto, informe explicitamente.</critical>

Se não for necessário dividir a tarefa:
- Explique por que a entrega deve seguir como um único fluxo.
- Justifique que a implementação é coesa e pequena o suficiente para ser entregue e validada como uma única unidade de valor.