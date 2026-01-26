# Django — Settings (Uso Prático)

Este documento define **como eu organizo e configuro settings em projetos Django**.

O objetivo é manter:
- previsibilidade entre ambientes (dev/staging/prod)
- segurança (segredos fora do código)
- clareza (settings fáceis de ler e manter)
- mudanças controladas ao longo do tempo

Settings são parte da arquitetura.
E precisam de governança.

---

## 🎯 Objetivo dos settings

Settings devem:

- ser fáceis de entender e modificar
- deixar explícito o que muda por ambiente
- evitar segredos no repositório
- reduzir “efeito dominó” quando o projeto cresce

---

## 🧠 Princípios que eu sigo

- **segredo nunca entra no Git**
- **ambientes são explícitos** (dev / prod)
- **configuração vem do ambiente** (env vars)
- **defaults seguros** (principalmente em produção)
- **settings pequenos e organizados**

---

## 🗂️ Organização recomendada

Prefiro separar settings por ambiente.

Exemplo:

config/
└── settings/
├── init.py
├── base.py
├── dev.py
├── prod.py
└── test.py


### `base.py`
Contém o comum entre ambientes:
- INSTALLED_APPS base
- MIDDLEWARE base
- templates/base config
- settings gerais (timezone, language, static/media)
- logging base

### `dev.py`
Dev local:
- DEBUG=True
- console email backend
- ferramentas de debug (se usadas)
- DB local
- permissões mais flexíveis (com consciência)

### `prod.py`
Produção:
- DEBUG=False
- ALLOWED_HOSTS obrigatório
- cookies/headers seguros
- DB e serviços externos via env
- logging mais robusto

### `test.py`
Testes:
- DB/engine adequado para testes
- performance e isolamento
- settings que deixam testes previsíveis

---

## 🔐 Variáveis de ambiente (env)

Tudo que for:
- segredo
- dependente de ambiente
- integração externa
deve vir via env.

Exemplos comuns:
- SECRET_KEY
- DATABASE_URL
- DEBUG
- ALLOWED_HOSTS
- CSRF_TRUSTED_ORIGINS
- EMAIL_* / SMTP
- SENTRY_DSN

Regra prática:
> Se eu não posso publicar isso, vai para env.

---

## 🧭 Como escolho o settings ativo

Eu escolho via variável de ambiente.

Exemplo conceitual:
- `DJANGO_SETTINGS_MODULE=config.settings.dev`
- `DJANGO_SETTINGS_MODULE=config.settings.prod`

Isso evita:
- if/else gigante dentro do settings
- comportamentos surpresa

---

## ✅ Regras mínimas de segurança (produção)

Em produção, garantir:

- `DEBUG = False`
- `SECRET_KEY` via env
- `ALLOWED_HOSTS` definido
- `CSRF_TRUSTED_ORIGINS` se necessário
- `SECURE_SSL_REDIRECT` (se aplicável)
- `SESSION_COOKIE_SECURE = True` (se aplicável)
- `CSRF_COOKIE_SECURE = True` (se aplicável)
- headers de segurança avaliados

> Não confiar em defaults do Django sem revisar.

---

## 📦 Static / Media (regra prática)

Definir claramente:

- `STATIC_URL`, `STATIC_ROOT`
- `MEDIA_URL`, `MEDIA_ROOT`

E separar responsabilidades:
- em dev pode servir local
- em prod deve ser servido por infra (ex: Nginx, CDN, storage)

---

## 🧾 Logging (mínimo viável)

Regras práticas:
- dev: logging legível no console
- prod: logs estruturados (ou pelo menos consistentes)
- erros importantes devem ser capturáveis (Sentry etc. se usado)

Evitar:
- logs silenciosos em produção
- log “barulhento” sem utilidade

---

## 🧪 Settings de testes (previsibilidade)

Em testes, priorizo:

- isolamento (um teste não pode depender de outro)
- previsibilidade (mesmos resultados sempre)
- velocidade (quando possível)

Exemplos de decisões comuns:
- email backend em memória
- cache simplificado
- configurações que removem chamadas externas

---

## 🚫 Anti-padrões comuns

Evitar:

- settings únicos gigantes (`settings.py` com 500 linhas)
- segredos no repositório
- lógica complexa dentro de settings
- “consertar prod” adicionando gambiarras no settings
- depender de comportamento implícito por ambiente

---

## 🔄 Mudanças em settings devem ser decisão

Mudança de settings em produção normalmente implica:
- impacto de segurança
- impacto operacional
- risco de indisponibilidade

Quando uma mudança for importante,
registrar decisão em `architecture/decisions.md`.

---

## 📚 Relação com outros documentos

- `django/project-structure.md`
- `architecture/decisions.md`
- `docker/compose.md` (quando settings dependem de serviços)
- `python/pyproject.md` (deps relacionadas)

---

## 📌 Nota final

Settings bons não são os “perfeitos”.
São os que evitam surpresa e reduzem risco.