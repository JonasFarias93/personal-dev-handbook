# Python — uv (Uso Prático)

Este documento descreve **como uso `uv`** no dia a dia.
Ele responde **como** gerenciar ambiente — não qual escolher.
Para decidir entre `venv` e `conda`, consulte `python/venv-vs-conda.md`.

`uv` não é moda.
É decisão de previsibilidade e redução de fricção.

---

# 🎯 Problema que o uv resolve

Sem uma ferramenta oficial, é comum ter:

* Múltiplas formas de instalar dependências
* Ambientes inconsistentes
* Comandos diferentes por projeto
* Setup lento e sujeito a erro
* Dependência excessiva de documentação para rodar o projeto

`uv` resolve isso ao:

* Centralizar ambiente + dependências
* Usar `pyproject.toml` como fonte de verdade
* Padronizar comandos

---

# 🧠 Princípio central

> Uma forma oficial de instalar, rodar e testar o projeto.

Se existem várias formas "válidas" de rodar o projeto,
nenhuma é realmente confiável.

---

# 🧩 Papel do uv no meu fluxo

O `uv` atua como:

* Gerenciador de dependências
* Criador de ambiente virtual
* Executor de comandos
* Interface única para tooling Python

Ele substitui:

* `pip` manual
* `pip-tools`
* Criação manual de `venv`
* Scripts frágeis de setup

Ele não substitui:

* `pyproject.toml`
* Docker
* CI
* Arquitetura do projeto

---

# 🐍 Relação com venv

`uv` usa `venv` por baixo.

Isso significa:

* Continua compatível com tooling Python
* Não altera fundamentos do ecossistema
* Não cria ambiente proprietário

Regra prática:

> Usar `uv` é usar `venv` de forma automatizada e consistente.

---

# 📦 Relação com `pyproject.toml`

`pyproject.toml` continua sendo a fonte de verdade:

* Dependências
* Dependências de desenvolvimento
* Configuração de ferramentas

`uv`:

* Lê o `pyproject.toml`
* Instala exatamente o que está definido
* Respeita grupos de dependência

Nenhuma dependência deve ser instalada "por fora".

---

# ⚙️ Fluxo padrão de uso

## Instalar ambiente e dependências
uv sync

Isso:

* Cria ambiente virtual se não existir
* Instala dependências declaradas

---

## Rodar comandos

Sempre uso:
uv run python manage.py runserver
uv run pytest
uv run black .

Isso garante:

* Ambiente correto ativo
* Nenhuma dependência vazada do sistema
* Comportamento previsível

---

## Adicionar dependência
uv add requests

Dependência de desenvolvimento:
uv add --dev pytest

`pyproject.toml` é atualizado automaticamente.

---

# 🧪 Relação com testes

Testes sempre rodam via:
uv run pytest

Benefícios:

* Evita erro de ambiente
* Garante dependências corretas
* Reduz variação entre máquinas

---

# 🐳 Relação com Docker

No meu fluxo:

* `uv` é ferramenta local
* Docker é ambiente de container

Dockerfile não depende de `uv`.

Regras:

* Ambiente local → `uv`
* Ambiente container → Dockerfile + Compose

Separação clara evita acoplamento desnecessário.

---

# 🤖 Relação com CI

Em CI posso:

* Usar `uv` para acelerar setup
* Ou usar `pip` direto, se simplificar pipeline

Decisão depende de:

* Tempo de execução
* Suporte do runner
* Simplicidade operacional

Localmente, `uv` é padrão oficial.

---

# 🚫 Quando NÃO usar uv

Evito usar quando:

* Projeto extremamente simples
* Ambiente já é rigidamente controlado por outra ferramenta
* Time não aceita dependência adicional

Ferramenta só vale se houver alinhamento consciente.

---

# 🚫 Anti-padrões

Evitar:

* Misturar `pip install` com `uv`
* Rodar comandos fora do `uv run`
* Instalar dependência sem atualizar `pyproject.toml`
* Tratar `uv` como opcional
* Versionar `.venv`

---

# 🧠 Checklist rápido

Antes de considerar uso correto:

* `pyproject.toml` é fonte de verdade
* Dependências são adicionadas via `uv add`
* Comandos rodam via `uv run`
* Não há `pip install` manual
* `.venv` está fora do Git

---

# 🗂 Fonte da Verdade

* `pyproject.toml` define dependências
* `uv` instala exatamente o declarado
* Ambiente virtual é descartável e recriável
* Tags representam versão oficial do projeto

Se ambiente divergir do declarado:

1. Recriar com `uv sync`
2. Revisar dependências no `pyproject.toml`

---

# 📚 Relação com outros documentos

* `python/venv-vs-conda.md` — qual ambiente escolher
* `python/pyproject.md` — declaração de dependências
* `docker/_dockerfile.md` — ambiente de container

---

# 📌 Nota final

`uv` reduz decisões repetidas.

Menos escolhas no setup →
mais energia para resolver o problema.
