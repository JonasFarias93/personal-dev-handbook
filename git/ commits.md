# Commits — Guia Pessoal de Uso

Este documento define **como e por que eu escrevo commits**.

O objetivo não é seguir moda ou ferramenta específica,
mas manter um **histórico legível, útil e sustentável**,
especialmente em projetos de médio e longo prazo.

---

## 🎯 Objetivo dos commits

Um commit deve registrar:

- **uma intenção clara**
- **uma mudança coerente**
- **um passo lógico na evolução do projeto**

Commit não é “salvar código”.  
Commit é **contar a história do projeto**.

---

## 🧠 Regra fundamental

> **Um commit = uma intenção**

Se não consigo explicar o commit em uma frase,
ele está grande demais.

---

## 🏷️ Padrão adotado

Adoto o padrão **Conventional Commits**, com escopo explícito.

Formato:

<tipo>(escopo): mensagem curta


---

## 🧩 Tipos utilizados

- `feat` — nova funcionalidade
- `fix` — correção de bug
- `refactor` — refatoração sem mudança de comportamento
- `docs` — documentação
- `test` — testes
- `chore` — infra, setup, dependências, tooling
- `style` — formatação (sem impacto lógico)

---

## 🎯 Escopo — como escolher

O escopo indica **onde a mudança aconteceu**.

Pode representar:

- camada: `web`, `domain`, `config`
- app/módulo: `chamado`, `execucao`, `cadastro`
- infra: `docker`, `deps`, `ci`

Exemplos válidos:

feat(chamado): adiciona regra de finalização
fix(config): corrige carregamento do dotenv
chore(docker): adiciona postgres ao compose
docs(architecture): documenta separação web/domain


---

## ✅ Bons exemplos

feat(domain): impede finalização de chamado sem itens
refactor(chamado): extrai validação para método privado
test(chamado): cobre regra de finalização
docs(git): documenta padrão de commits


---

## ❌ Anti-padrões

Nunca usar mensagens genéricas como:

update
ajustes
fix
testes
initial commit


Esses commits:

- não comunicam intenção
- não ajudam no futuro
- empobrecem o histórico

---

## 🧪 Commits e testes

Regra prática:

- `feat` → idealmente acompanhado de teste
- `fix` → teste que reproduz o bug
- `refactor` → testes existentes devem continuar passando

---

## 🧠 Regra de validação rápida

Antes de confirmar um commit, pergunte:

- Esse commit tem **um propósito claro**?
- Ele faz **uma coisa só**?
- O escopo está correto?
- Eu entenderia isso daqui a 6 meses?

Se sim → commit ok.
