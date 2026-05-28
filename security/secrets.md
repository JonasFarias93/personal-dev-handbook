# Security — Gestão de Segredos

Este documento define **como gerencio segredos e variáveis sensíveis**
em projetos Django.

Segredo exposto é incidente.
Não é descuido.

---

# 🎯 Objetivo

* Nunca expor segredos no repositório
* Tornar explícito o que é sensível
* Padronizar gestão de `.env` entre projetos
* Reduzir risco operacional

---

# 🧠 Princípio central

> Se não posso publicar, vai para variável de ambiente.

Sem exceção.

---

# 🚫 O que nunca entra no Git

* `SECRET_KEY`
* Credenciais de banco (`DATABASE_URL`, usuário, senha)
* Tokens de API (Stripe, SendGrid, AWS, etc.)
* `SENTRY_DSN`
* Qualquer senha ou chave privada
* Arquivo `.env`

Regra prática:

> Se tem "key", "secret", "password", "token" ou "dsn" no nome — é segredo.

---

# 🗂 Estrutura padrão de arquivos
projeto/
├── .env            # real — fora do Git
├── .env.example    # template — entra no Git
└── .gitignore      # garante que .env não vaze

`.gitignore` mínimo obrigatório:
.env
*.env

---

# 📋 `.env.example` — padrão de escrita

O `.env.example` entra no Git como template.

Regras:

* Nunca colocar valor real
* Usar placeholder descritivo
* Documentar variáveis não óbvias com comentário

Exemplo:
Django
DJANGO_SETTINGS_MODULE=config.settings.dev
SECRET_KEY=your-secret-key-here
DEBUG=1
ALLOWED_HOSTS=localhost,127.0.0.1
Banco de dados
DATABASE_URL=postgres://user:password@db:5432/dbname
Cache
REDIS_URL=redis://redis:6379/0
Email (opcional em dev)
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
Monitoramento (opcional)
SENTRY_DSN=your-sentry-dsn-here

---

# ⚙️ Como o Django lê variáveis de ambiente

Padrão sem biblioteca externa:

```python
import os

SECRET_KEY = os.environ.get("SECRET_KEY")
DATABASE_URL = os.environ.get("DATABASE_URL")
DEBUG = os.environ.get("DEBUG", "0") == "1"
```

Atenção:

* `os.environ.get()` sempre retorna string
* Booleanos precisam de conversão explícita
* Variável ausente retorna `None` silenciosamente — validar quando crítico

Alternativa futura a avaliar:

* `django-environ` ou `python-decouple` fazem casting automático
* Útil quando o projeto crescer e settings ficarem mais complexos

---

# 🐳 Relação com Docker

No Compose, variáveis vêm do `.env` via `env_file`:

```yaml
web:
  env_file:
    - .env
```

Regras:

* `.env` nunca entra no Git
* `.env.example` documenta o que o container precisa
* Variáveis do container não devem ser hardcoded no `docker-compose.yml`

---

# 🤖 Relação com CI

Em CI, segredos vêm de **GitHub Secrets** — nunca de arquivo commitado.

Exemplo no workflow:

```yaml
- name: Tests
  env:
    SECRET_KEY: ${{ secrets.SECRET_KEY }}
    DATABASE_URL: ${{ secrets.DATABASE_URL }}
  run: uv run pytest
```

Regra:

> CI não lê `.env`. CI lê secrets do repositório.

---

# ✅ Checklist antes de commit

* `.env` está no `.gitignore`
* Nenhum segredo hardcoded no código
* `.env.example` está atualizado
* Nenhuma credencial em `settings.py`, `docker-compose.yml` ou YAML de CI
* `git diff` revisado antes de push

---

# 🚫 Anti-padrões

Evitar:

* `SECRET_KEY = "valor-real"` em qualquer arquivo commitado
* Credenciais em comentários de código
* `.env` commitado "só dessa vez"
* Segredo em variável com nome genérico (`KEY`, `PASS`)
* Compartilhar segredo via chat ou e-mail

---

# 🗂 Fonte da Verdade

* `.env` define configuração local
* GitHub Secrets define configuração de CI
* `.env.example` documenta o contrato de variáveis
* ADR registra decisão estrutural relevante

Se um segredo vazar:

1. Revogar imediatamente
2. Gerar novo valor
3. Atualizar todos os ambientes
4. Revisar histórico Git (`git log`, `git diff`)

---

# 📚 Relação com outros documentos

* `security/django.md` — configurações de segurança do Django em produção
* `django/settings.md` — organização de settings por ambiente
* `docker/compose.md` — uso de `env_file` no Compose
* `workflow/ci.md` — uso de GitHub Secrets no pipeline

---

# 📌 Nota final

Segredo no repositório não é erro de ferramenta.
É erro de processo.

Checklist antes de commit custa 30 segundos.
Incidente de segurança custa muito mais.
