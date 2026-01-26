# Docker Compose — Uso Prático

Este documento define como eu uso **Docker Compose** para desenvolvimento local.

O objetivo é:
- reduzir fricção de setup (onboarding rápido)
- padronizar serviços (db/cache/broker)
- deixar o ambiente reproduzível
- evitar “na minha máquina funciona”

---

## 🎯 Quando usar Docker Compose

Uso Compose quando o projeto depende de:
- banco (Postgres/MySQL)
- cache (Redis)
- filas (RabbitMQ)
- serviços auxiliares (Mailhog, MinIO etc.)

Se o projeto é 100% simples (só Python puro), posso não usar.

---

## 🧠 Princípios que eu sigo

- Compose é para **dev**, não “produção disfarçada”
- Configuração via **env** (segredo não entra no Git)
- Serviços têm nomes previsíveis: `db`, `redis`, `web`
- Persistência local com volumes nomeados
- Healthcheck sempre que fizer sentido (evita corrida de inicialização)

---

## 🧱 Estrutura recomendada

docker/
├── compose.md
├── dockerfile.md
└── debugging.md

docker-compose.yml
.env.example


- `docker-compose.yml` na raiz (mais fácil pra comandos)
- documentação dentro de `docker/`

---

## ✅ Compose base (Django + Postgres + Redis)

Exemplo de `docker-compose.yml` para dev:

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
🔐 .env e .env.example
Regras:

.env fica fora do Git

.env.example entra no Git e serve de template

Exemplo de .env.example:

DJANGO_SETTINGS_MODULE=config.settings.dev
DATABASE_URL=postgres://app:app@db:5432/app
REDIS_URL=redis://redis:6379/0
SECRET_KEY=dev-only-change-me
DEBUG=1
🔁 Comandos essenciais
Subir o ambiente:

docker compose up -d --build
Ver logs:

docker compose logs -f web
Entrar no container:

docker compose exec web bash
Rodar migrações:

docker compose exec web python manage.py migrate
Derrubar tudo:

docker compose down
Derrubar removendo volumes (zera o banco):

docker compose down -v



🧩 Boas práticas que eu sigo
Volumes

usar volume nomeado para banco (pgdata)

código montado como bind mount (.:/app) para hot reload

Portas

expor portas só do que eu preciso acessar do host

manter padrão: 8000 web, 5432 postgres, 6379 redis

depends_on

preferir condition: service_healthy quando disponível

evita “web subiu mas DB ainda não”

🚫 Anti-padrões comuns

Evitar:

colocar segredo no docker-compose.yml

usar Compose como “produção”

depender de ordem de start sem healthcheck

rodar tudo como root sem necessidade

persistir estado crítico sem volume (perde dados sem querer)

✅ Checklist rápido

Antes de commitar mudanças no Compose:

 serviços têm nomes consistentes (db, redis, web)

 .env.example atualizado

 segredos não foram adicionados no Git

 volumes corretos (db persistente, código montado)

 healthcheck em serviços críticos (db/cache)

