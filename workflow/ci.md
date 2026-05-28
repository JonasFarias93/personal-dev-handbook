# CI — Integração Contínua (Padrão Oficial)

Este documento define o **padrão oficial de CI (Continuous Integration)**
adotado nos meus projetos.

CI não é apenas automação.
É um **mecanismo de governança de qualidade**.

---

# 🎯 Objetivo da CI

A CI existe para:

* Detectar erro cedo
* Garantir que a branch principal esteja saudável
* Proteger contra regressões
* Automatizar validações repetitivas
* Reduzir dependência de revisão manual básica

CI não substitui revisão.
CI impede erro óbvio.

---

# 🧠 Princípio central

> Nada entra na branch principal quebrando o mínimo aceitável de qualidade.

Se algo quebra na CI,
o merge não deve acontecer.

---

# 🗂 Quando a CI roda

Padrão oficial:

* Em todo Pull Request
* Em push para `develop`
* Opcionalmente em push para `main`

Não rodar CI apenas em release.
Qualidade deve ser contínua.

---

# ⚙️ O que a CI deve executar (mínimo obrigatório)

## 1️⃣ Instalação do ambiente

* Setup Python
* Instalação de dependências via `uv`

## 2️⃣ Lint

* Ruff

## 3️⃣ Testes

* `pytest`
* Falha bloqueia merge

## 4️⃣ Type-check

* `mypy`

---

# 🧩 Workflow de referência (Django + uv)

Este é o workflow base usado nos projetos.
Salvar em `.github/workflows/ci.yml`.

```yaml
name: CI

on:
  pull_request:
  push:
    branches:
      - develop

jobs:
  ci:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install uv
        run: pip install uv

      - name: Install dependencies
        run: uv sync

      - name: Lint (ruff)
        run: uv run ruff check .

      - name: Type-check (mypy)
        run: uv run mypy .

      - name: Tests (pytest)
        env:
          DJANGO_SETTINGS_MODULE: config.settings.test
        run: uv run pytest
```

Ajustar `python-version` e `DJANGO_SETTINGS_MODULE` conforme o projeto.

---

# 🚦 Política de bloqueio

Bloqueia merge quando:

* Testes falham
* Lint falha
* Type-check falha
* Setup não executa corretamente

Não bloquear por:

* Métricas vaidosas
* Cobertura arbitrária sem critério

Qualidade > burocracia.

---

# 🔁 Relação com Definition of Done

CI valida parte da DoD automaticamente.

Exemplo:

* Testes passando
* Código formatado
* Lint limpo
* Types verificados

CI é braço automatizado da DoD.

---

# 🐳 Relação com Docker

CI não substitui Docker.

Possíveis estratégias:

* Testar diretamente no runner (padrão)
* Ou buildar imagem Docker e testar dentro dela

Escolha depende do projeto.
Backend web tende a manter setup simples.

---

# 🧪 Relação com Testes

Se testes são lentos demais,
CI ficará lenta.

Arquitetura deve permitir:

* Testes unitários rápidos
* Integrações isoladas
* Pipeline previsível

Se CI está sofrendo,
rever arquitetura ou estratégia de teste.

---

# 🏷 Relação com Releases

Antes de promover para `main`:

* CI deve estar verde
* Branch de integração deve estar estável

Tag nunca deve ser criada com pipeline quebrado.

---

# 🗂 Fonte da Verdade

* Workflow YAML em `.github/workflows/ci.yml`
* `pyproject.toml` define dependências e configuração de ferramentas
* `workflow/DoD.md` define critérios humanos

Se houver divergência:

1. Revisar pipeline
2. Revisar DoD
3. Registrar decisão em ADR se estrutural

---

# 🚫 Anti-padrões

Evitar:

* Pipeline gigante desde o primeiro dia
* Ferramentas demais sem necessidade
* Bloqueios excessivos
* Ignorar CI quebrada
* "Arrumar depois" na branch principal

---

# 📈 Evolução consciente

CI deve evoluir junto com o projeto.

Adicionar etapas quando:

* Complexidade aumentar
* Time crescer
* Risco justificar

Não adicionar por moda.

---

# 📚 Relação com outros documentos

* `workflow/DoD.md` — critérios humanos que a CI complementa
* `python/uv.md` — interface de ambiente usada no pipeline
* `git/branching.md` — branches que disparam a CI

---

# 📌 Nota final

CI é contrato automático de qualidade.

Se a CI está sempre verde mas bugs continuam,
o problema não é a ferramenta.
É o critério.
