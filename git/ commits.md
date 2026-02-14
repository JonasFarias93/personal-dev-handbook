# Commits — Guia Pessoal de Uso

Este documento define **como e por que escrevo commits**,
alinhado com clareza histórica, governança e versionamento consciente.

Commit não é "salvar código".
É registrar intenção arquitetural.

---

# 🎯 Objetivo dos commits

Um commit deve registrar:

* Uma intenção clara
* Uma mudança coerente
* Um passo lógico na evolução do projeto
* Um ponto rastreável da história

Commit conta a história do projeto.

---

# 🧠 Regra fundamental

> Um commit = uma intenção.

Se não consigo explicar o commit em uma frase,
ele está grande demais.

---

# 🏷️ Padrão adotado

Adoto **Conventional Commits** com escopo explícito.

Formato:

```
<tipo>(escopo): mensagem curta
```

Mensagem curta deve:

* Estar no imperativo
* Ser objetiva
* Não terminar com ponto final

---

# 🧩 Tipos utilizados

* `feat` — nova funcionalidade
* `fix` — correção de bug
* `refactor` — refatoração sem mudança de comportamento
* `docs` — documentação
* `test` — testes
* `chore` — infra, setup, dependências, tooling
* `style` — formatação sem impacto lógico

---

# 🎯 Escopo — como escolher

Escopo indica onde a mudança ocorreu.

Pode representar:

* Contexto: `chamado`, `execucao`, `iam`
* Camada: `domain`, `web`, `config`
* Infra: `docker`, `deps`, `ci`
* Documento: `architecture`, `git`, `docker`

Exemplos válidos:

```
feat(chamado): adiciona regra de finalizacao
fix(config): corrige carregamento do dotenv
chore(docker): adiciona postgres ao compose
docs(architecture): documenta separacao web/domain
```

---

# ✅ Bons exemplos

```
feat(domain): impede finalizacao de chamado sem itens
refactor(chamado): extrai validacao para metodo privado
test(chamado): cobre regra de finalizacao
docs(git): documenta padrao de commits
```

---

# ❌ Anti-padrões

Evitar mensagens como:

```
update
ajustes
fix
testes
initial commit
```

Esses commits:

* Não comunicam intenção
* Não ajudam no futuro
* Empobrecem o histórico

---

# 🧪 Commits e testes

Regra prática:

* `feat` → idealmente acompanhado de teste
* `fix` → deve incluir teste que reproduz o bug
* `refactor` → testes existentes continuam passando

Se o comportamento muda, testes devem refletir isso.

---

# 🔄 Commits e Versionamento (SemVer)

Commits influenciam versionamento:

* `feat` → pode gerar incremento MINOR
* `fix` → normalmente PATCH
* Mudança que quebra contrato → exige decisão consciente (possível MAJOR)

Se a mudança for estrutural relevante,
registrar ADR antes ou junto ao commit.

---

# 🧠 Regra de validação rápida

Antes de confirmar um commit, pergunte:

* Ele tem um propósito claro?
* Faz uma coisa só?
* O escopo está correto?
* Eu entenderia isso daqui a 6 meses?
* Ele conversa com a versão atual do projeto?

Se sim → commit adequado.

---

# 🗂 Fonte da Verdade

* O histórico Git é fonte primária da evolução
* ADR registra decisões estruturais
* Versão do projeto deve refletir impacto real das mudanças

Se o commit altera arquitetura relevante,
verificar se há ADR correspondente.

---

# 📌 Nota final

Histórico limpo reduz retrabalho futuro.

Commit bom hoje é tempo economizado amanhã.
