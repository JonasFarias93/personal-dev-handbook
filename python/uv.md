# Python — uv (Uso Prático e Decisão Consciente)

Este documento descreve **como e por que eu uso o `uv`**
como ferramenta padrão para gerenciamento de ambiente e dependências Python.

O objetivo é:
- reduzir fricção no setup local
- acelerar instalação de dependências
- padronizar comandos do dia a dia
- evitar combinações frágeis (`pip + venv + scripts soltos`)

`uv` não é moda.
É uma **decisão de produtividade e previsibilidade**.

---

## 🎯 O problema que o uv resolve

Sem uma ferramenta clara, é comum ter:

- múltiplas formas de instalar dependências
- ambientes inconsistentes entre devs
- comandos diferentes por projeto
- setup lento e propenso a erro
- dependência de documentação extensa para rodar o projeto

O `uv` resolve isso ao:
- centralizar ambiente + dependências
- usar `pyproject.toml` como fonte de verdade
- padronizar comandos

---

## 🧠 Princípio central

> **Uma forma oficial de instalar, rodar e testar o projeto.**

Se existem várias formas “válidas” de rodar o projeto,
na prática nenhuma é confiável.

---

## 🧩 O que é o uv (no meu uso)

No meu fluxo, o `uv` atua como:

- gerenciador de dependências
- criador de ambiente virtual
- executor de comandos
- interface única para tooling Python

Ele **substitui**:
- `pip`
- `pip-tools`
- criação manual de `venv`
- scripts frágeis de setup

Ele **não substitui**:
- `pyproject.toml`
- Docker
- CI
- arquitetura do projeto

---

## 🐍 Relação com `venv`

O `uv` **usa `venv` por baixo**.

Isso significa:
- não cria um “novo tipo” de ambiente
- continua compatível com tooling Python
- não muda conceitos fundamentais

Regra prática:
> Usar `uv` é usar `venv` de forma automatizada e consistente.

---

## 📦 Relação com `pyproject.toml`

O `pyproject.toml` continua sendo a **fonte de verdade**:

- dependências
- dependências de desenvolvimento
- configuração de ferramentas

O `uv`:
- lê o `pyproject.toml`
- instala exatamente o que está definido ali
- respeita grupos (`optional-dependencies`)

Nenhuma dependência deve ser instalada “por fora”.

---

## ⚙️ Fluxo padrão de uso (dia a dia)

### Criar ambiente e instalar dependências

```bash
uv sync
Isso:

cria o ambiente virtual (se não existir)

instala dependências do projeto

instala dependências de desenvolvimento (quando configuradas)

Rodar comandos do projeto
Sempre uso uv run:

uv run python manage.py runserver
uv run pytest
uv run black .
Isso garante:

ambiente correto ativo

nenhuma dependência “vazada” do sistema

comportamento previsível

Adicionar dependência
uv add requests
Dependência de desenvolvimento:

uv add --dev pytest
O pyproject.toml é atualizado automaticamente.

🧪 Relação com testes
Testes sempre rodam via uv:

uv run pytest
Benefícios:

elimina “pytest não encontrado”

garante dependências corretas

reduz variação entre máquinas

🐳 Relação com Docker
No meu fluxo:

uv é usado localmente

Docker continua sendo a fonte de verdade para containers

Dockerfile não depende de uv

Regras práticas:

ambiente local → uv

ambiente container → Dockerfile + Compose

Isso evita acoplamento desnecessário.

🤖 Relação com CI
Em CI, posso:

usar uv para acelerar setup

ou usar pip direto (dependendo do ambiente)

Decisão depende de:

tempo de pipeline

suporte do runner

simplicidade desejada

Localmente, uv é sempre preferido.

🚫 Quando NÃO usar uv
Evito usar uv quando:

projeto é puramente educacional muito simples

ambiente já é totalmente controlado por outra ferramenta

time não aceita dependência adicional (decisão consciente)

Ferramenta só vale se o time comprar a ideia.

🚫 Anti-padrões comuns
Evitar:

misturar pip install com uv

rodar comandos fora do uv run

instalar dependência sem atualizar pyproject.toml

tratar uv como “detalhe opcional”

usar uv e ainda depender de .venv manual

🧠 Checklist rápido
Antes de considerar o uso do uv correto:

 pyproject.toml é a fonte de verdade

 dependências são adicionadas via uv add

 comandos rodam via uv run

 não existe pip install manual

 .venv continua fora do Git

📌 Nota final
uv não é sobre velocidade apenas.
É sobre reduzir decisões repetidas.

Menos escolhas no setup →
mais energia para resolver o problema real.