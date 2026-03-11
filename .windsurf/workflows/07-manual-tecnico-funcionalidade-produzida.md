---
description: 
---
## Inputs

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="TASK_PLAN_NAME">
  Nome do arquivo do Task Plan a ser lido para recuperar contexto da feature.
</instrucao>

Obtenha o contexto da tarefa lendo o arquivo que contém o plano de implementação através do <TASK_PLAN_NAME> que é o nome do arquivo que foi digitado após a instrução /07-manual-tecnico-funcionalidade-produzida.md <MICROSSERVICO> <TASK_PLAN_NAME>. Se precisar de mais contexto, leia o PRD e a Tech Spec relacionados.

Gere uma documentação técnica da feature produzida.

**1. Recuperação de contexto:**
- Relacione o que foi implementado com o conteúdo de PRD e Tech Spec

**2. Conteúdo da documentação:**
- Explique de forma objetiva o propósito da feature.
- Destaque decisões técnicas e de lógica relevantes.
- Liste pontos importantes do código (classes, métodos, endpoints, regras, etc), sem exibir o código completo.
- Informe como a feature interage com outros módulos do sistema, se aplicável.

**3. Testes:**
- Descreva os testes implementados para validar a feature (unitários, integração, etc).
- Indique como os testes cobrem os critérios de aceite.
- Não inclua o código dos testes.

**4. Restrições:**
- Não invente ou assuma informações ausentes.
- Não utilize emojis ou elementos gráficos.
- Utilize um estilo direto, técnico e claro.

**Formato da saída:** Markdown bem estruturado, com seções claras como `## Visão Geral`, `## Decisões Técnicas`, `## Pontos Relevantes do Código`, `## Testes`, `## Validação de Critérios de Aceite`.

Importante: não invente informações.