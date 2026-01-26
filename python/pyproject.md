# Python — pyproject.toml (Uso Prático)

Este documento descreve **como eu uso `pyproject.toml`** para organizar projetos Python.

O objetivo é:
- padronizar setup de projetos
- centralizar configurações de tooling
- reduzir arquivos soltos (`setup.py`, `setup.cfg`, etc.)
- deixar o projeto previsível e fácil de manter

`pyproject.toml` é a **fonte de verdade** do projeto Python.

---

## 🎯 Por que usar pyproject.toml

Uso `pyproject.toml` porque ele:

- centraliza metadados do projeto
- define dependências de forma clara
- concentra configuração de ferramentas (formatador, linter, testes)
- é o padrão moderno do ecossistema Python

Evito misturar:
- `requirements.txt` + `setup.py` + `setup.cfg`
quando o projeto já pode nascer com `pyproject.toml`.

---

## 🧠 Princípios que eu sigo

- um projeto → um `pyproject.toml`
- tooling configurado no próprio projeto
- dependências separadas por contexto (runtime / dev)
- versões explícitas quando faz sentido
- simplicidade antes de otimização prematura

---

## 🧱 Estrutura mínima de um projeto Python

project/
├── pyproject.toml
├── README.md
├── src/ | apps/
├── tests/
└── .venv/ # fora do Git


---

## 📦 Estrutura base do pyproject.toml

Exemplo de estrutura mínima e funcional:

```toml
[project]
name = "meu-projeto"
version = "0.1.0"
description = "Descrição curta do projeto"
readme = "README.md"
requires-python = ">=3.11"

dependencies = [
    "django>=5.0",
]

---

[project.optional-dependencies]
dev = [
    "pytest",
    "pytest-django",
    "black",
    "ruff",
    "mypy",
]
🧩 Dependências (regra prática)
dependencies
tudo que a aplicação precisa para rodar

usado em produção

deve ser o mínimo necessário

optional-dependencies.dev
ferramentas de desenvolvimento

testes, lint, formatação

nunca dependências de runtime

Regra mental:

se o código roda sem isso em produção, vai para dev.

🧰 Configuração de ferramentas (tooling)
Centralizo o máximo possível no pyproject.toml.

Black (formatação)
[tool.black]
line-length = 88
target-version = ["py311"]
Ruff (lint)
[tool.ruff]
line-length = 88
select = ["E", "F", "W"]
ignore = ["E501"]
Pytest
[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
Mypy (tipagem)
[tool.mypy]
python_version = "3.11"
ignore_missing_imports = true
strict = false
🧪 Relação com testes
pytest é a base

configuração vive no pyproject.toml

evita arquivos espalhados (pytest.ini, setup.cfg, etc.)

Testes são parte do projeto, não acessório.

🔄 Versionamento do projeto
Uso versionamento simples:

início: 0.x.x

estabilidade inicial: 1.0.0

evoluções seguem SemVer

A versão do projeto não precisa mudar a cada commit.
Ela muda em releases.

🚫 Anti-padrões comuns
Evitar:

requirements.txt gigante sem critério

tooling configurado fora do projeto sem motivo

dependências duplicadas (pip install manual)

versões totalmente soltas quando estabilidade importa

misturar dependência de dev com runtime

🧠 Checklist rápido
Antes de considerar o pyproject.toml ok:

 nome e versão fazem sentido

 dependências mínimas em dependencies

 tooling em optional-dependencies.dev

 configurações centralizadas

 .venv fora do Git

📌 Nota final
Se o setup do projeto é confuso,
o código tende a ficar confuso depois.

pyproject.toml bem feito economiza
tempo, erro e retrabalho.