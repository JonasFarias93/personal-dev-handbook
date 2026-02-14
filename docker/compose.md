# Docker Compose — Uso Prático

Este documento define como utilizo **Docker Compose para desenvolvimento local**,
alinhado com previsibilidade, governança e separação clara entre dev e produção.

Compose é ferramenta de orquestração de ambiente.
Não é produção disfarçada.

---

# 🎯 Quando usar Docker Compose

Uso Compose quando o projeto depende de:

* Banco de dados (Postgres/MySQL)
* Cache (Redis)
* Fila (RabbitMQ)
* Serviços auxiliares (Mailhog, MinIO, etc.)

Se o projeto for simples (sem dependências externas), posso optar por não usar.

---

# 🧠 Princípios que sigo

* Compose é para desenvolvimento local
* Configuração vem de variáveis de ambiente (.env)
* Segredos nunca entram no Git
* Serviços têm nomes previsíveis (`db`, `redis`, `web`)
* Persistência local usa volumes nomeados
* Serviços críticos possuem healthcheck
* Mudanças estruturais relevantes podem exigir ADR

---

# 🧱 Estrutura recomendada

```
docker/
├── compose.md
├── dockerfile.md
└── debugging.md


docker-compose.yml
.env.example
```

* `docker-compose.yml` fica na raiz (facilita comandos)
* Documentação dentro de `docker/`

---

# ✅ Compose base (Django + Postgres + Redis)

Exemplo para desenvolvimento:

```yaml
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_DB: app
      POSTGRES_USER: app
      POSTGRES_PASSWORD: app
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app -d app"]
      interval: 5s
      timeout: 5s
      retries: 10

  redis:
    image: redis:7
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      timeout: 3s
      retries: 10

  web:
    build:
      context: .
      dockerfile: Dockerfile
    env_file:
      - .env
    command: python manage.py runserver 0.0.0.0:8000
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy

volumes:
  pgdata:
```

---

# 🔐 `.env` e `.env.example`

Regras:

* `.env` fica fora do Git
* `.env.example` entra no Git como template

Exemplo de `.env.example`:

```
DJANGO_SETTINGS_MODULE=config.settings.dev
DATABASE_URL=postgres://app:app@db:5432/app
REDIS_URL=redis://redis:6379/0
SECRET_KEY=dev-only-change-me
DEBUG=1
```

---

# 🔁 Comandos essenciais

Subir ambiente:

```
docker compose up -d --build
```

Ver logs:

```
docker compose logs -f web
```

Entrar no container:

```
docker compose exec web bash
```

Rodar migrações:

```
docker compose exec web python manage.py migrate
```

Derrubar:

```
docker compose down
```

Remover volumes (zera banco):

```
docker compose down -v
```

---

# 🧩 Boas práticas que sigo

## Volumes

* Banco usa volume nomeado (`pgdata`)
* Código usa bind mount (`.:/app`) para hot reload

## Portas

* Expor apenas o necessário
* Padrão comum:

  * 8000 → web
  * 5432 → postgres
  * 6379 → redis

## depends_on

* Preferir `condition: service_healthy`
* Evita corrida de inicialização

---

# 🚫 Anti-padrões que evito

* Colocar segredo no `docker-compose.yml`
* Usar Compose como ambiente de produção
* Depender de ordem de start sem healthcheck
* Rodar tudo como root sem necessidade
* Persistir banco sem volume

---

# ✅ Checklist rápido

Antes de commitar mudanças no Compose:

* Serviços têm nomes consistentes (`db`, `redis`, `web`)
* `.env.example` está atualizado
* Nenhum segredo foi adicionado ao Git
* Volumes estão corretos
* Serviços críticos têm healthcheck

---

# 🗂 Fonte da Verdade

* `docker-compose.yml` real no repositório é fonte primária
* `.env` define configuração de ambiente
* Dockerfile define ambiente de execução
* ADR registra decisões estruturais relevantes

Se a documentação divergir do código:

1. Código prevalece
2. Documento deve ser atualizado
3. Se estrutural, registrar novo ADR

---

# 📌 Nota final

Compose bem feito reduz fricção,
acelera onboarding
e elimina inconsistências de ambiente.

Se está complexo demais,
provavelmente está fazendo mais do que deveria.
