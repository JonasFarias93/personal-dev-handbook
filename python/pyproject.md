# Python — pyproject.toml (Uso Prático)

Este documento descreve **como utilizo `pyproject.toml`** para organizar projetos Python,
alinhado com previsibilidade, governança e versionamento consciente.

`pyproject.toml` é a fonte de verdade do projeto Python.

---

# 🎯 Por que usar pyproject.toml

Uso `pyproject.toml` porque ele:

* Centraliza metadados do projeto
* Define dependências de forma explícita
* Concentra configuração de tooling
* É o padrão moderno do ecossistema Python

Evito misturar:

* `requirements.txt`
* `setup.py`
* `setup.cfg`

quando o projeto pode nascer diretamente com `pyproject.toml`.

---

# 🧠 Princípios que sigo

* Um projeto → um `pyproject.toml`
* Tooling configurado dentro do próprio projeto
* Dependências separadas por contexto (runtime / dev)
* Versões explícitas quando estabilidade importa
* Simplicidade antes de abstração prematura
* Versão do projeto alinhada com SemVer

---

# 🧱 Estrutura mínima de um projeto Python

```
project/
├── pyproject.toml
├── README.md
├── web/ ou src/
├── tests/
└── .venv/  # fora do Git
```

---

# 📦 Estrutura base do pyproject.toml

Exemplo mínimo funcional:

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

[project.optional-dependencies]
dev = [
    "pytest",
    "pytest-django",
    "black",
    "ruff",
    "mypy",
]
```

---

# 🧩 Dependências (regra prática)

## dependencies

* Tudo que a aplicação precisa para rodar
* Usado em produção
* Deve ser o mínimo necessário

## optional-dependencies.dev

* Ferramentas de desenvolvimento
* Testes, lint, formatação
* Nunca dependências de runtime

Regra mental:

> Se o código roda em produção sem isso, vai para dev.

---

# 🧰 Configuração de ferramentas (Tooling)

Centralizo o máximo possível no `pyproject.toml`.

## Black

```toml
[tool.black]
line-length = 88
target-version = ["py311"]
```

## Ruff

```toml
[tool.ruff]
line-length = 88
select = ["E", "F", "W"]
ignore = ["E501"]
```

## Pytest

```toml
[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
```

## Mypy

```toml
[tool.mypy]
python_version = "3.11"
ignore_missing_imports = true
strict = false
```

Evito espalhar configuração em múltiplos arquivos sem necessidade.

---

# 🧪 Relação com testes

* `pytest` é base padrão
* Configuração vive no `pyproject.toml`
* Testes são parte estrutural do projeto

Se o projeto exige `pytest.ini`, justificar a decisão.

---

# 🔄 Versionamento do projeto

Uso SemVer:

* Início → `0.x.x`
* Marco estável → `1.0.0`
* Evoluções seguem MAJOR.MINOR.PATCH

A versão do projeto muda em releases,
não a cada commit.

Tags devem refletir a versão definida aqui.

---

# 🚫 Anti-padrões que evito

* `requirements.txt` gigante sem critério
* Tooling configurado fora do projeto sem motivo
* Dependência instalada manualmente sem declarar
* Versões totalmente soltas quando estabilidade importa
* Misturar dependência de dev com runtime

---

# 🧠 Checklist rápido

Antes de considerar o `pyproject.toml` adequado:

* Nome e versão fazem sentido
* Dependências mínimas em `dependencies`
* Tooling em `optional-dependencies.dev`
* Configurações centralizadas
* `.venv` fora do Git
* Versão alinhada com release atual

---

# 🗂 Fonte da Verdade

* `pyproject.toml` define metadados e dependências
* Ambiente virtual instala exatamente o que está declarado
* Tags devem refletir a versão definida
* ADR registra decisões estruturais relevantes

Se houver divergência entre ambiente e `pyproject.toml`:

1. `pyproject.toml` deve ser corrigido
2. Ambiente deve ser recriado

---

# 📌 Nota final

Se o setup do projeto é confuso,
o código tende a ficar confuso depois.

`pyproject.toml` bem estruturado economiza tempo,
reduz erro
e fortalece governança técnica.
