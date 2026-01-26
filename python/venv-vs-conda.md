# Python — venv vs Conda (Decisão Consciente)

Este documento registra **como eu escolho e uso ambientes Python**
(`venv` ou `conda`) de forma consciente.

O objetivo não é defender ferramenta,
mas **escolher a ferramenta certa para o contexto certo**,
evitando confusão, retrabalho e setups frágeis.

Ambiente é infraestrutura.
E infraestrutura é decisão.

---

## 🎯 O problema que isso resolve

Sem uma decisão clara sobre ambiente, é comum surgir:

- conflito de dependências
- versões diferentes entre máquinas
- “funciona pra mim”
- setups difíceis de reproduzir
- perda de tempo configurando ambiente

Este documento existe para **evitar esse caos**.

---

## 🧠 Princípio central

> **Ambiente deve ser simples, previsível e reproduzível.**

Se o ambiente exige explicação longa,
ele provavelmente está errado para aquele projeto.

---

## 🐍 `venv` — quando eu uso

Uso **`venv`** quando:

- projeto é **backend/web** (Django, FastAPI, Flask)
- dependências são majoritariamente Python puro
- deploy usa Docker ou ambiente Linux padrão
- quero simplicidade e alinhamento com produção
- o projeto será compartilhado com outros devs

### Vantagens do `venv`

- nativo do Python
- simples de entender
- amplamente conhecido
- funciona muito bem com Docker
- menos “mágica”

### Limitações

- dependências de sistema precisam ser resolvidas fora
- menos amigável para libs científicas pesadas

---

## 🧪 `conda` — quando eu uso

Uso **Conda** quando:

- trabalho com **ciência de dados**
- uso bibliotecas com dependências nativas pesadas
  (NumPy, SciPy, TensorFlow, etc.)
- preciso gerenciar versões de Python + libs não-Python
- o ambiente não será dockerizado

### Vantagens do Conda

- resolve dependências binárias complexas
- ótimo para data science
- ambientes isolados completos
- menos dor com libs científicas

### Limitações

- mais pesado
- menos alinhado com produção web
- não costuma refletir o ambiente final de deploy
- menos comum em times backend tradicionais

---

## 🧠 Regra prática que eu sigo

- **Backend / Web / APIs** → `venv`
- **Data Science / ML / Pesquisa** → `conda`

Evito misturar os dois no mesmo projeto.

---

## 🧱 Como eu organizo com `venv`

Padrão:

project/
├── .venv/ # fora do Git
├── pyproject.toml
├── README.md
└── src/


Regras:
- `.venv` nunca entra no Git
- dependências declaradas no `pyproject.toml`
- setup documentado no README

---

## 🧱 Como eu organizo com Conda

Padrão:

- ambiente criado com nome do projeto
- arquivo `environment.yml` documentado
- dependências claras e versionadas

Uso Conda **quando ele resolve um problema real**,
não por hábito.

---

## 🚫 Anti-padrões comuns

Evitar:

- usar Conda só “porque sim”
- usar `venv` com libs científicas pesadas sem necessidade
- misturar pip + conda sem entender
- não documentar como criar o ambiente
- depender de ambiente global

---

## 🔄 Relação com Docker

Quando uso Docker:

- o ambiente local (`venv` ou conda) é secundário
- o Dockerfile vira a fonte de verdade
- o importante é que **o código rode igual**

Por isso, em projetos backend,
`venv + Docker` costuma ser a combinação ideal.

---

## 🧠 Checklist rápido de decisão

Antes de escolher, eu pergunto:

- este projeto vai para produção web?
- usa libs científicas pesadas?
- será dockerizado?
- outras pessoas vão rodar isso?

Se:
- web + docker → `venv`
- ciência de dados → `conda`

---

## 📌 Nota final

Ambiente não é preferência pessoal.
É **decisão técnica baseada em contexto**.

Escolher bem aqui economiza
tempo, energia e dor de cabeça depois.