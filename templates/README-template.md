# <Nome do Projeto>

> Uma linha descrevendo o que o projeto faz e para quem.

---

## 🎯 Objetivo

Descrever:

* Que problema resolve
* Para quem
* O que está fora do escopo

---

## 🧱 Stack

* **Linguagem:**
* **Framework:**
* **Banco de dados:**
* **Cache:**
* **Infra:**

---

## 🚀 Como rodar localmente

### Pré-requisitos

* Python 3.12+
* Docker e Docker Compose
* uv

### Setup

```bash
# 1. Clonar o repositório
git clone 
cd 

# 2. Copiar variáveis de ambiente
cp .env.example .env

# 3. Subir serviços
docker compose up -d --build

# 4. Rodar migrações
docker compose exec web python manage.py migrate

# 5. Rodar a aplicação
docker compose up
```

---

## ⚙️ Variáveis de ambiente

Consultar `.env.example` para lista completa.

Variáveis obrigatórias:

| Variável | Descrição |
|---|---|
| `SECRET_KEY` | Chave secreta do Django |
| `DATABASE_URL` | URL de conexão com o banco |
| `DJANGO_SETTINGS_MODULE` | Módulo de settings ativo |

---

## 🧪 Testes

```bash
uv run pytest
```

---

## 🧰 Comandos úteis

```bash
# Lint
uv run ruff check .

# Type-check
uv run mypy .

# Migrações
docker compose exec web python manage.py migrate

# Shell Django
docker compose exec web python manage.py shell

# Logs
docker compose logs -f web
```

---

## 🗂 Estrutura do projeto
<projeto>/
├── config/
├── <app>/
├── tests/
├── docker/
├── pyproject.toml
└── docker-compose.yml

---

## 📚 Documentação interna

* `architecture/` — decisões arquiteturais e ADRs
* `CONTRIBUTING.md` — como contribuir

---

## 🚧 Status

`Em desenvolvimento` | `Beta` | `Produção`

---
