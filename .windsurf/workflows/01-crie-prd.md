---
description: 
---

## 1. Obter contexto da tarefa

Utilize este arquivo de prompt (workflow) para obter o contexto da tarefa após o nome deste arquivo ser mencionado.
Deverá ser atribuído a <DATA-ATUAL> a seguinte máscara yyyy-MM-dd-HH-mm, sendo yyyy-MM-dd-HH-mm a data e hora atual.
O contexto da tarefa poderá ser extraído de duas maneiras:
1. Através de um texto no prompt através do seguinte comando: /01-crie-prd.md <MICROSSERVICO> <TEXTO DO CONTEXTO DA TAREFA>
Por exemplo: será digitado no prompt /01-crie-prd.md temperature-monitoring crie um endpoint para... . 

2. Através de um arquivo que contém um texto que será obtido com o seguinte comando: /01-crie-prd.md <MICROSSERVICO> <ARQUIVO DO CONTEXTO DA TAREFA>
Por exemplo: será digitado no prompt /01-crie-prd.md temperature-monitoring @nome-do-arquivo. 

<critical>
  Este workflow deve delegar a geração do PRD para a skill registrada `skill-generate-prd`.
  Referência: `.windsurf/skills/skill-generate-prd/SKILL.md`.
</critical>
<critical>
  Após obtido o contexto da tarefa, crie um arquivo de PRD (PT-BR) conforme instruções contidas na skill registrada.
  Não realize nenhuma implementação.
</critical>

## Inputs

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="TEXTO DO CONTEXTO DA TAREFA">
  É o texto que informará a descrição da tarefa. O texto poderá estar no próprio prompt ou ser um arquivo que conterá o contexto da tarefa.
</instrucao>

<instrucao id="ARQUIVO DO CONTEXTO DA TAREFA">
  Leia o arquivo mencionado para obter o contexto da tarefa.
</instrucao>

## Fluxo de Trabalho

Ao ser invocado com uma solicitação de funcionalidade, siga esta sequência:

### 1. Esclarecer (Obrigatório)
Faça perguntas para entender:
- Problema a resolver
- Funcionalidade principal

### 2. Planejar (Obrigatório)
Crie um plano de desenvolvimento do PRD incluindo:
- Abordagem seção por seção
- Áreas que precisam pesquisa
- Premissas e dependências

### 3. Redigir o PRD (Obrigatório)
- Use a estrutura e regras definidas na skill registrada `skill-generate-prd`
- Foque no O QUÊ e POR QUÊ, não no COMO
- Inclua requisitos funcionais numerados
- Mantenha o documento principal com  no máximo 1.000 palavras

### 4. Criar Diretório e Salvar (Obrigatório)
- Crie o diretório e salve o PRD conforme regras definidas na skill registrada `skill-generate-prd`

### 5. Reportar Resultados
- Forneça o caminho do arquivo final
- Resumo das decisões tomadas
- Questões em aberto

<critical>NÃO GERE O PRD SEM ANTES FAZER PERGUNTAS DE CLARIFICAÇÃO</critical>
<critical>NÃO INVENTE INFORMAÇÕES. SE ALGO ESTIVER AUSENTE NO CONTEXTO, INFORME EXPLICITAMENTE</critical>