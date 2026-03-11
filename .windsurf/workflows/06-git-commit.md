---
description: 
---

Utilize este workflow para gerar uma mensagem de commit seguindo Conventional Commits.

Exemplo de invocação:
`06-git-commit <MICROSSERVICO>`

### **Entradas:**

<instrucao id="MICROSSERVICO">
  O valor <MICROSSERVICO> será algo como `device-management`, `temperature-monitoring`, `temperature-processing`.
</instrucao>

<critical>
  O commit deve ser feito apenas no <MICROSSERVICO> definido.
  Antes de confirmar, valide que os arquivos staged estão restritos a `microservices/<MICROSSERVICO>/`.
</critical>

1.  **Tipo de mudança:**
    * `feat`: Uma nova funcionalidade.
    * `fix`: Uma correção de bug.
    * `docs`: Mudanças de documentação.
    * `style`: Mudanças de formatação (espaços, ponto e vírgula etc.).
    * `refactor`: Mudança de código que não corrige bug e não adiciona funcionalidade.
    * `test`: Adição ou correção de testes.
    * `chore`: Mudanças no processo de build ou ferramentas auxiliares.

2.  **Escopo (Opcional):**
    * A parte do codebase afetada (ex.: `api`, `ui`, `auth`, `payment`). Isso ajuda a especificar o contexto da mudança.

3.  **Descrição curta:**
    * Uma frase curta, no imperativo, que resume a mudança (ex.: "Adicionar funcionalidade de login").

4.  **Descrição detalhada (Opcional):**
    * Uma descrição mais longa do que foi alterado e por quê. Pode incluir o contexto da mudança, os problemas que resolve ou seus impactos.

---

### **Instruções para a IA:**

Com base nas "Entradas" e em uma análise das mudanças no repositório, faça o seguinte:

1.  **Linha de assunto:**
    * Crie uma única linha de assunto no formato: `<type>(<scope>): <short_description>`.
    * O escopo é opcional. Se não for informado, use o formato: `<type>: <short_description>`.
    * Use verbos no imperativo, como "add", "fix", "update", "improve".

2.  **Corpo da mensagem:**
    * Se uma "Descrição detalhada" for fornecida, adicione uma linha em branco após a linha de assunto e insira o texto detalhado.
    * A descrição deve explicar o **porquê** da mudança, e não apenas o que foi alterado.

3.  **Idioma:**
    * Todas as mensagens geradas devem estar em **Inglês**.

---

### **Exemplos de saída:**

* **Exemplo 1 (Sem escopo):**
    `fix: correct validation error on contact form`

* **Exemplo 2 (Com escopo):**
    `feat(api): add new endpoint for user data`

* **Exemplo 3 (Com escopo e descrição detalhada):**
    `refactor(ui): improve button component styles

    Refactors the styling of the primary button component to use CSS variables. This change improves consistency across the application and makes future style updates easier to manage.`

Execute o comando para confirmar o commit com esta mensagem. Se o parâmetro `--no-verify` for adicionado ao comando `/git-commit`, não execute os hooks.