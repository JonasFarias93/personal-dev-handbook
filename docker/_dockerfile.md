# Dockerfile — Guia Pessoal

Este documento define **como eu escrevo Dockerfiles** para projetos
(principalmente Python/Django).

O foco é:
- builds previsíveis
- imagens menores e seguras
- ambiente coerente com o Docker Compose
- facilidade de debug no dia a dia

Dockerfile não é só infra.
É parte da arquitetura.

---

## 🎯 Quando este padrão se aplica

Uso este padrão quando:

- o projeto roda com Docker Compose
- preciso de ambiente local reproduzível
- quero evitar “na minha máquina funciona”
- o projeto tende a crescer ou ser mantido por mais tempo

Para scripts simples ou projetos muito pequenos,
posso optar por não usar Docker.

---

## 🧠 Princípios que eu sigo

- Dockerfile deve ser **legível**
- Ordem das instruções importa (cache de build)
- Dependências vêm antes do código
- Configuração vem do ambiente (env vars)
- Segredos **não entram no Dockerfile**
- Sempre que possível, rodar como usuário não-root

---

## 🧱 Estrutura esperada do projeto

.
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── .env.example
├── manage.py
├── pyproject.toml | requirements.txt
└── src/ | apps/


---

## 📦 `.dockerignore` (obrigatório)

Sempre usar `.dockerignore` para evitar builds lentos
e imagens desnecessariamente grandes.

Exemplo mínimo:

.git
pycache
*.pyc
*.pyo
*.pyd
.env
.venv
venv
.envrc
.pytest_cache
.mypy_cache
.coverage
node_modules


---

## 🏗️ Dockerfile base (Python / Django — dev)

Este Dockerfile é **pensado para desenvolvimento local**,
em conjunto com o `docker-compose.yml`.

```dockerfile
# syntax=docker/dockerfile:1

FROM python:3.12-slim

# Evita arquivos .pyc e garante logs imediatos
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Dependências do sistema (ajustar conforme o projeto)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
  && rm -rf /var/lib/apt/lists/*

# Copiar dependências primeiro (cache de build)
# Usar UM dos dois: pyproject.toml OU requirements.txt

# Exemplo com requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install --upgrade pip \
 && pip install -r /app/requirements.txt

# Copiar o código depois
COPY . /app

# Criar usuário não-root
RUN useradd -m appuser \
 && chown -R appuser:appuser /app

USER appuser

# Comando padrão (dev)
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
🔁 Relação com o Docker Compose
Este Dockerfile assume que:

variáveis vêm de .env (env_file no compose)

o código será montado como volume (.:/app)

o serviço se chama web

banco/cache são serviços externos (db, redis)

O Dockerfile não conhece banco, redis ou settings.
Isso é responsabilidade do Compose + env.

🧪 Dev vs Produção (regra clara)
Este Dockerfile não é para produção.

Em produção, normalmente:

não monto volume de código

uso gunicorn/uvicorn

posso usar multi-stage

imagem é mais enxuta

DEBUG = False obrigatoriamente

Essas decisões devem ser documentadas
em um Dockerfile específico de produção ou no architecture/decisions.md.

🚫 Anti-padrões comuns
Evitar:

copiar o projeto inteiro antes de instalar dependências

colocar SECRET_KEY, tokens ou senhas no Dockerfile

usar latest sem critério

rodar tudo como root sem necessidade

criar Dockerfile “mágico” difícil de entender

✅ Checklist rápido
Antes de considerar o Dockerfile ok:

 existe .dockerignore

 dependências são instaladas antes do código

 não há segredos no Dockerfile

 roda como usuário não-root

 comando (CMD) é coerente com o ambiente (dev)

 sobe corretamente via docker compose up

📌 Nota final
Se o Dockerfile ficou difícil de entender,
ele já está errado.

Simplicidade aqui reduz bugs,
acelera onboarding
e economiza tempo no futuro.