---
name: skill-generate-techspec
description: Gerar Tech Spec a partir do PRD (baseado em template)
---

# Skill - Gerar Tech Spec

<critical>
  Após obter o contexto da tarefa a partir do PRD, crie um arquivo de Tech Spec seguindo as instruções de template definidas nesta skill.
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

## Referência do Template

<instrucao id="TECHSPEC_TEMPLATE">
  Arquivo fonte do template de Tech Spec: `.ai-templates/technical-specifications.md`
</instrucao>

## Saída

<instrucao id="TECHSPEC_NAME">
  Nome do arquivo final: `tech-spec-<DATA-ATUAL>.md`
</instrucao>

<instrucao id="TECHSPEC_DIRECTORY">
  Diretório final: `/microservices/<MICROSSERVICO>/.ai-templates/<DATA-ATUAL>-[nome-funcionalidade]/technical-specifications/` (nome da funcionalidade em kebab-case)
</instrucao>

## Fluxo de Trabalho

### 1. Analisar PRD (Obrigatório)
- Leia o PRD por completo
- Extraia requisitos principais, restrições, métricas de sucesso e fases de rollout
- Identifique e sinalize conteúdo técnico que deva ser movido para a Tech Spec

### 2. Análise Profunda do Repositório (Obrigatório)
- Descubra arquivos/módulos/interfaces/pontos de integração envolvidos
- Mapeie dependências e pontos de risco
- Verifique persistência, concorrência, tratamento de erros, configs, testes e implicações de infraestrutura

### 3. Esclarecimentos Técnicos (Obrigatório)
Faça perguntas focadas sobre:
- Propriedade/limites do domínio
- Fluxo de dados e contratos
- Dependências externas e modos de falha
- Interfaces principais
- Foco de testes

### 4. Mapeamento de Conformidade com Padrões (Obrigatório)
- Mapeie decisões para `@padroes-codigo.md`
- Destaque desvios com justificativa e alternativas conformes

### 5. Gerar Tech Spec (Obrigatório)
- Use `TECHSPEC_TEMPLATE` como estrutura exata
- Foque em COMO implementar (evite repetir requisitos do PRD)
- Inclua: visão geral da arquitetura, componentes, interfaces, modelos, endpoints, integrações, análise de impacto, estratégia de testes, observabilidade
- Mantenha com até ~2.000 palavras

### 6. Salvar Tech Spec (Obrigatório)
- Salve em `TECHSPEC_DIRECTORY` como `TECHSPEC_NAME`

### 7. Protocolo de Saída
Na mensagem final:
1. Resumo das decisões
2. Conteúdo completo da Tech Spec (Markdown)
3. Caminho onde a Tech Spec foi salva
4. Questões em aberto e próximos passos

<critical>Não invente informações. Se algo estiver ausente, informe explicitamente.</critical>
