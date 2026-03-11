---
name: skill-generate-prd
description: Gerar PRD a partir do contexto (baseado em template)
---

# Skill - Gerar PRD

<critical>
  Após obter o contexto da tarefa, crie um arquivo de PRD seguindo as instruções de template definidas nesta skill.
  Não implemente código.
</critical>

## Entradas

<instrucao id="MICROSSERVICO">
  Valor como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="TEXTO DO CONTEXTO DA TAREFA">
  Texto descrevendo o contexto da tarefa.
</instrucao>

<instrucao id="DATA-ATUAL">
  Valor com máscara `yyyy-MM-dd-HH-mm` e deve ser a data/hora atual. Exemplo: `2026-02-22-16-59`.
</instrucao>

## Referência do Template

<instrucao id="PRD_TEMPLATE">
  Arquivo fonte do template de PRD: `.ai-templates/product-requirements.md`
</instrucao>

## Saída

<instrucao id="PRD_NAME">
  Nome do arquivo final: `prd-<DATA-ATUAL>.md`
</instrucao>

<instrucao id="PRD_DIRECTORY">
  Diretório final: `/microservices/<MICROSSERVICO>/.ai-templates/<DATA-ATUAL>-[nome-funcionalidade]/product-requirements/` (nome da funcionalidade em kebab-case)
</instrucao>

## Fluxo de Trabalho

### 1. Esclarecer (Obrigatório)
Faça perguntas para entender:
- Problema a resolver
- Funcionalidade principal
- Restrições
- Fora de escopo

<critical>Não gere o PRD antes das perguntas de esclarecimento serem respondidas.</critical>

### 2. Planejar (Obrigatório)
Crie um plano seção por seção para escrever o PRD:
- Abordagem por seção
- Informações ausentes que devem ser fornecidas
- Premissas e dependências

### 3. Redigir o PRD (Obrigatório)
- Use `PRD_TEMPLATE` como estrutura exata
- Foque no O QUÊ e POR QUÊ (não no COMO)
- Inclua requisitos funcionais numerados
- Mantenha o documento principal com até ~1.000 palavras

### 4. Criar Diretório e Salvar (Obrigatório)
- Crie `PRD_DIRECTORY`
- Salve o PRD como `PRD_NAME`

### 5. Protocolo de Saída
Na mensagem final:
1. Conteúdo completo do PRD (Markdown)
2. Caminho onde o PRD foi salvo
3. Questões em aberto para stakeholders

<critical>Não invente informações. Se algo estiver ausente, informe explicitamente.</critical>