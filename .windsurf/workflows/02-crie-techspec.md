---
description: 
---

## 2. Criar um plano de implementação com base na tarefa

Utilize este arquivo de prompt (workflow) criar uma technical specification, com o seguinte comando: /02-crie-techspec.md <MICROSSERVICO> <PRD_NAME>
Por exemplo: será digitado no prompt /02-crie-techspec.md temperature-monitoring @nome-do-prd
 
 <critical>
   Este workflow deve delegar a geração da Tech Spec para a skill registrada `skill-generate-techspec`.
   Referência: `.windsurf/skills/skill-generate-techspec/SKILL.md`.
 </critical>
 
 <critical>
   Após obtido o contexto da tarefa, crie um arquivo de technical specification (PT-BR) conforme instruções contidas neste arquivo.
   Não realize nenhuma implementação.
 </critical>

## Inputs

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="PRD_NAME">
  Nome do arquivo do PRD a ser lido (gerado no passo 01).
</instrucao>
 
 ## Fluxo de Trabalho
 
### 1. Ler o PRD informado (Obrigatório)

### 2. Fazer perguntas técnicas de clarificação (Obrigatório)

### 3. Gerar e salvar a Tech Spec conforme a skill registrada (Obrigatório)

<critical>Faça perguntas de clarificação, caso seja necessário, ANTES de criar o arquivo final</critical>
<critical>Não invente informações. Se algo estiver ausente no contexto, informe explicitamente.</critical>