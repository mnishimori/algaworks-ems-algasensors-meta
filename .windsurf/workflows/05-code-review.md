---
description: 
---

# Code Review - Análise Automatizada de MRs (v1.1)

**Contexto:** Spring Boot + React/TypeScript + DDD

---

## 📋 Pré-requisitos

- **Arquitetura:** Domain-Driven Design (Domain, Infrastructure, Presentation)

---

## 🔧 Mapeamento de Ferramentas MCP

| Etapa | MCP Server | Tool | Função |
|-------|------------|------|--------|
| 4.1 | local | analyze_architecture | Avalia Arquitetura DDD |
| 4.2 | local | analyze_backend | Avalia Qualidade Backend |
| 4.3 | local | analyze_frontend | Avalia Qualidade Frontend |
| 4.4 | local | analyze_database | Avalia Banco de Dados & Persistência |
| 4.5 | local | analyze_api | Avalia REST API & Segurança |
| 4.6 | local | analyze_performance | Avalia Escalabilidade & Performance |
| 4.7 | local | analyze_test | Avalia criação de testes para novas Classes |
| 4.8 | local | analyze_checkstyle | Avalie o checkstyle do projeto |
| 4.9 | local | analyze_codestyle | Avalie o codestyle do projeto |
| 5 | gitlab | create_merge_request_note | Publica relatório consolidado |
| 6 | gitlab | create_merge_request_thread | Cria threads inline |

---

```yaml
instructions:
  - "Identificar e revisar os códigos alterados na branch atual, seja de classes ou métodos, independente se foram versionados."
  - "Não alterar código do MR."
  - "Gerar apenas comentários e threads inline."
  - "Explicar problema, impacto e sugerir correção sem modificar arquivos."
  - "Seguir prioridade F/C/B e limite de threads dinâmico."
  - "Evitar duplicidade de threads para problemas similares."
```

---

## Inputs

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<instrucao id="TASK_PLAN_NAME">
  Nome do arquivo do Task Plan a ser lido para recuperar contexto e critérios da mudança.
</instrucao>

---

## Workflow (EXECUÇÃO SEQUENCIAL OBRIGATÓRIA)

---
### **ETAPA 1: Obtenha o contexto da tarefa**
 
Leia o arquivo do plano de implementação através do <TASK_PLAN_NAME> que é o nome do arquivo que foi digitado após a instrução /05-code-review.md <MICROSSERVICO> <TASK_PLAN_NAME>. Se precisar de mais contexto, leia o PRD e a Tech Spec relacionados.
 
**VALIDAÇÃO:**
- ✅ Encontrado → ETAPA 2
- ❌ Erro → PARAR: "MR não encontrado"

---

### **ETAPA 4: Análise de Código Modularizada**

**Arquivos analisados:** `<mr_files>`
**6 Módulos Independentes**

---

#### **4.1 Arquitetura DDD**
**Tool:** `analyze_architecture`
**Checklist:** Domain, Services, Repositories, Controllers, Infra, Pacotes
**Rubrica:** A+ → F
**OUTPUT:** `architecture_result: {nota, status, problemas}`

---

#### **4.2 Qualidade Backend**
**Tool:** `analyze_backend`
**Checklist:** 
  - SOLID, 
  - nomenclatura, 
  - constructor injection, 
  - logs, 
  - imutabilidade, 
  - validação
  - não permita import de classes e interfaces não utilizadas
  - a declaração de variáveis/objetos deve ser por inferência, utilizando a palavra reservada var, evitando a declaração explícita do tipo da classe.
  - avalie as regras na rule @geracao-classes-architecture.md.
  - avalie as regras na rule @padroes-codigo.md.
  - avalie as regras de check style contidas em @checkstyle.xml e caso necessário aponte as inconsistências no relatório de correções encontradas no code review
  - aplique as regras de code style contidas em @codestyle.xml e caso necessário aponte as inconsistências no relatório de correções encontradas no code review
**Rubrica:** A → F
**OUTPUT:** `backend_result: {nota, status, problemas}`

---

#### **4.3 Qualidade Frontend**
**Tool:** `analyze_frontend`
**Checklist:** Hooks, TypeScript strict, console, memory leaks, React Query, acessibilidade
**Rubrica:** A → F
**OUTPUT:** `frontend_result: {nota, status, problemas}`

---

#### **4.4 Banco de Dados & Persistência**
**Tool:** `analyze_database`
**Checklist:** Migrations, índices, queries, rollback, criptografia, transações
**Rubrica:** A → F
**OUTPUT:** `database_result: {nota, status, problemas}`

---

#### **4.5 REST API & Segurança**
**Tool:** `analyze_api`
**Checklist:** DTOs, REST, versionamento, validação, OAuth2, CORS, rate limiting
**Rubrica:** A → F
**OUTPUT:** `api_result: {nota, status, problemas}`

---

#### **4.6 Escalabilidade & Performance**
**Tool:** `analyze_performance`
**Checklist:** Backend e Frontend: stateless, cache, async, memory leaks, lazy loading, otimização de re-renders
**Rubrica:** A → F
**OUTPUT:** `performance_result: {nota, status, problemas}`

---

#### **4.7 Criação de testes para novas Classes**
**Tool:** `analyze_test`
**Checklist:** 
- Verifica se classes novas possuem testes correspondentes
- Avalie as regras na rule @padroes-codigo-de-teste.md.
- Analisa Java (JUnit) e TypeScript (Jest/RTL)
- Ignora Config, DTO e Migration
- Valida estrutura:
  - `src/main/java/.../Xxx.java`  --> `src/test/java/.../XxxTest.java`
  - `src/main/typescript/src/components/.../Xxx.tsx` --> `src/main/typescript/src/__tests__/Xxx.test.tsx` ou `Xxx.spec.tsx`

**Rubrica:** A → F
**OUTPUT:** `tests_result: {nota, status, problemas}`

**REGRAS DE THREAD:**
- **Prioridade:** C (Importante)
- **Máximo:** 5 threads por MR
- **Linha específica do diff obrigatória**
- **Mensagem padrão:**

```markdown
🤖 [TEST COVERAGE - C] Classe sem teste correspondente

**Problema:** A classe `<nome>`  foi criada sem teste automatizado.  
**Impacto:** Reduz cobertura e dificulta detecção de regressões.  
**Sugestão:** Crie `<nome>Test.java`  ou `<nome>.test.tsx` 
validando cenários principais.
```

---

#### **4.8 Checkstyle**
**Tool:** `analyze_checkstyle`  
**Checklist:**  
- Avalia se o código segue as regras definidas no arquivo `checkstyle.xml`
- Verifica indentação, nome de classes e métodos, tamanho de linhas, espaçamento, comentários e uso adequado de modificadores
- Identifica violações por gravidade (erro/aviso)

**Rubrica:** A → F  
**OUTPUT:** `checkstyle_result: {nota, status, problemas}`

---

#### **4.9 Codestyle**
**Tool:** `analyze_codestyle`  
**Checklist:**  
- Avalia conformidade com convenções do projeto (arquivo `codestyle.xml`)
- Verifica padrões de nomenclatura, uso de `var` em vez de declaração explícita, espaçamento interno, alinhamento e estrutura de blocos
- Sugere correções quando aplicável

**Rubrica:** A → F  
**OUTPUT:** `codestyle_result: {nota, status, problemas}`

---


### **ETAPA 5: Publicar Relatório**

**Tool:** `mcp0_create_merge_request_note`

**Regras**
- Considere a regra PUBLICACAO_GITLAB nesta etapa.

**Template com placeholders:**
```markdown
# 🤖 Code Review Automatizado - MR <merge_request_iid>

> ⚠️ Review gerado por IA - Revise criticamente

## 📊 Informações

| Critério | Valor | Status |
|----------|-------|--------|
| Ticket | {{ticket_key}} | ✅/❌ |
| Tipo | {{jira_type}} | - |
| Autor | {{mr_author}} | - |
| Arquivos | {{mr_files|count}} | - |
| Backend | {{backend_files_count}} | - |
| Frontend | {{frontend_files_count}} | - |
| Migrations | {{sql_files_count}} | - |

## 🎯 Avaliação

| Categoria | Nota | Status | Problemas |
|-----------|------|--------|-----------|
| Arquitetura DDD | {{architecture_result.nota}} | {{architecture_result.status}} | {{architecture_result.problemas}} |
| Qualidade Backend | {{backend_result.nota}} | {{backend_result.status}} | {{backend_result.problemas}} |
| Qualidade Frontend | {{frontend_result.nota}} | {{frontend_result.status}} | {{frontend_result.problemas}} |
| BD & Persistência | {{database_result.nota}} | {{database_result.status}} | {{database_result.problemas}} |
| REST & Segurança | {{api_result.nota}} | {{api_result.status}} | {{api_result.problemas}} |
| Escalabilidade | {{performance_result.nota}} | {{performance_result.status}} | {{performance_result.problemas}} |

**Críticos:** {{critical_count}} | **Importantes:** {{important_count}} | **Menores:** {{minor_count}}
```

**VALIDAÇÃO:**
- ✅ Publicado → ETAPA 6
- ❌ Erro → PARAR

---

### **ETAPA 6: Criar Threads Inline**

**Tool:** `mcp0_create_merge_request_thread`

**Prioridade ponderada:**
```yaml
prioridade:
  F: 3
  C: 2
  B: 1
```

**Regras:**
- Máx 20 threads por MR
- F (crítico) → sempre criar
- C → criar se threads criadas < 15
- B → criar se threads criadas < 20 e não duplicar problema
- Linha específica do diff obrigatória
- Problemas transversais → threads separadas
- Considere a regra PUBLICACAO_GITLAB nesta etapa.

**Template Comentário:**
```markdown
🤖 **[<CAT>] <Título>**

**Problema:** <descrição clara>
**Impacto:** <bugs/segurança/performance/manutenção/escalabilidade>
**Sugestão:**
```<lang>
<código ou referência>
```
**Refs:** <links docs Spring/React/padrões>

---
_Sugestão IA - Revise criticamente_
```

---

### **ETAPA 7: Logging Estruturado**

```yaml
echo "[INFO] Workflow finalizado"
echo "[INFO] Threads criadas: {{thread_count}}"
echo "[INFO] Críticos detectados: {{critical_count}}"
echo "[INFO] Status final MR: {{mr_status}}"
```

---

### 🔍 Troubleshooting

| Erro | Solução |
|------|---------|
| MR não encontrado | Verificar `project_id` e `merge_request_iid` |
| Jira indisponível | Prosseguir sem contexto |
| Diff grande | Priorizar `.java`, `.ts/.tsx`, `.sql` |
| Thread falha | Verificar `diff_refs` disponível |
| Timeout | Reduzir nº de threads (máx 10) |

---

## 📚 Referências

- **Spring Boot:** https://docs.spring.io/spring-boot/docs/current/reference/html/
- **Spring Security OAuth2:** https://docs.spring.io/spring-security/reference/servlet/oauth2/index.html
- **React:** https://react.dev/
- **TypeScript:** https://www.typescriptlang.org/docs/
- **Domain-Driven Design:** https://martinfowler.com/bliki/DomainDrivenDesign.html

---