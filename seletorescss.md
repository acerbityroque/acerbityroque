# 🧪 Quando o ID some... a gente dá um jeito! 💡
## Desvendando os seletores CSS no BugBank com Cypress

### 🕵️‍♂️ O problema real:
Na aplicação BugBank, a gente se deparou com o seguinte campo:

```diff
<input type="email" class="input__default" placeholder="Informe seu e-mail" name="email">
```

O mesmo elemento aparecia tanto na página de login quanto na de registro — no mesmo espaço!

➡️ Resultado: o Cypress ficava confuso e os testes **falhavam**.

### ❌ O que NÃO funcionava:
Tentamos os seletores \"óbvios\":

```diff
cy.get(input[name=\"email\"])
cy.get(.input__default)
cy.get([placeholder=\"Informe seu e-mail\"])
```

Nada disso funcionou com segurança. O teste não sabia qual input usar.

### ✅ O que salvou o rolê?
A solução foi usar os seletores de posição com **.eq():**

```diff
cy.get('.login__form input').eq(0).type('meuemail@example.com')
cy.get('.login__form input').eq(1).type('minhasenha123')
```

### 🧠 Explicando a técnica:
```diff
.login__form = isolamos o formulário
input = pegamos todos os inputs daquele bloco
.eq(número) = selecionamos com base na posição (ordem do elemento)
```

### 💡 Dica de ouro
Esse método é super útil quando:
```diff
✔️ Não tem ID disponível  
✔️ A estrutura da página é previsível  
✔️ Você quer testar inputs em blocos isolados
```

### ⚠️ Mas atenção: 
Se a ordem dos inputs mudar, seu teste pode quebrar!

