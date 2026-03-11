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

Obtenha o contexto da tarefa lendo o arquivo que contém o plano de implementação através do <TASK_PLAN_NAME> que é o nome do arquivo que foi digitado após a instrução /08-manual-produto-funcionalidade-produzida.md <MICROSSERVICO> <TASK_PLAN_NAME>. Se precisar de mais contexto, leia o PRD e a Tech Spec relacionados.

Gere uma descrição funcional da feature de software implementada, com o objetivo de servir de base para profissionais de Produto ou áreas de relacionamento com o cliente criarem manuais e comunicações voltadas ao usuário final.

**1. Contexto da tarefa:**
- Relacione o que foi implementado com o conteúdo de PRD e Tech Spec

**2. Conteúdo a ser gerado:**
- Descreva, de forma clara e acessível, qual problema essa feature resolve ou qual funcionalidade nova ela oferece ao usuário.
- Informe onde e como o usuário final interage com essa funcionalidade (ex: via tela X, menu Y, API, etc).
- Destaque pré-requisitos ou configurações necessárias para uso.
- Inclua limitações ou comportamentos esperados que possam gerar dúvidas.
- Evite linguagem técnica de implementação ou termos de código.

**3. Objetivo final:**
- Este conteúdo será usado como base para a produção de materiais como:
  - Manuais de uso
  - Comunicados de release notes
  - Documentação interna de produto

**4. Restrições:**
- Não inclua código-fonte, nomes de métodos ou detalhes técnicos internos.
- Não invente comportamento não descrito na tarefa.
- Não use emojis ou elementos visuais decorativos.
- Use linguagem acessível, com foco no usuário final.

**Formato da saída:** Markdown bem estruturado, com seções claras como `## Visão Geral`, `## Decisões Técnicas`, `## Testes`, `## Validação de Critérios de Aceite`.

Importante: não invente informações.