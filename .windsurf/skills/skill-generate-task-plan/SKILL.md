---
name: skill-generate-task-plan
description: Gerar Task Plan (dividir em MRs/tarefas) a partir de PRD + Tech Spec
---

# Skill - Gerar Task Plan

<critical>
  Após obter o contexto da tarefa a partir do PRD e da Tech Spec, crie um relatório de Task Plan seguindo as instruções definidas nesta skill.
  Não implemente código.
</critical>

## Entradas

<instrucao id="MICROSSERVICO">
  Valor como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="DATA-ATUAL">
  Valor com máscara `yyyy-MM-dd-HH-mm` e deve ser a data/hora atual. Exemplo: `2026-02-22-16-59`.
</instrucao>

<instrucao id="PRD_NAME">
  Nome do arquivo do PRD: `prd-<DATA-ATUAL>.md`
</instrucao>

<instrucao id="PRD_DIRECTORY">
  Diretório do PRD: `/microservices/<MICROSSERVICO>/.ai-templates/<DATA-ATUAL>-[nome-funcionalidade]/product-requirements/` (nome da funcionalidade em kebab-case)
</instrucao>

<instrucao id="TECHSPEC_NAME">
  Nome do arquivo da Tech Spec: `tech-spec-<DATA-ATUAL>.md`
</instrucao>

<instrucao id="TECHSPEC_DIRECTORY">
  Diretório da Tech Spec: `/microservices/<MICROSSERVICO>/.ai-templates/<DATA-ATUAL>-[nome-funcionalidade]/technical-specifications/` (nome da funcionalidade em kebab-case)
</instrucao>

## Saída

<instrucao id="TASK_PLAN_NAME">
  Nome do arquivo final: `task-plan-<DATA-ATUAL>.md`
</instrucao>

<instrucao id="TASK_PLAN_DIRECTORY">
  Diretório final: `/microservices/<MICROSSERVICO>/.ai-templates/<DATA-ATUAL>-[nome-funcionalidade]/task-plan/` (nome da funcionalidade em kebab-case)
</instrucao>

## Objetivo

Com base em `PRD_NAME` e `TECHSPEC_NAME`, avalie se a implementação deve ser dividida em múltiplos Merge Requests e/ou tarefas menores.

## Critérios para Divisão
- Alta complexidade ou alto risco técnico
- Componentes independentes ou paralelizáveis
- Facilitar code review e teste incremental
- Reduzir riscos de regressão
- Otimizar validação com QA/Produto

## Formato de Saída Esperado (Markdown)

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

## Observações
- Se não for necessário dividir, explique por que deve ser entregue como um único fluxo coeso.

<critical>Não invente informações. Se algo estiver ausente, informe explicitamente.</critical>
