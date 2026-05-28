markdown# Security — Django (Produção)

Este documento define **as configurações de segurança obrigatórias
para projetos Django em produção**.

Settings padrão do Django não são seguros por default.
Segurança em produção é configuração explícita.

---

# 🎯 Objetivo

* Tornar explícito o que deve ser configurado antes de ir a produção
* Reduzir risco operacional
* Evitar exposição por configuração negligenciada

---

# 🧠 Princípio central

> Em produção, nenhuma configuração de segurança deve depender de default.

Se não está explícito, não está garantido.

---

# ✅ Checklist obrigatório de produção

Antes de qualquer deploy em produção, verificar:

* `DEBUG = False`
* `SECRET_KEY` via variável de ambiente
* `ALLOWED_HOSTS` definido explicitamente
* `CSRF_TRUSTED_ORIGINS` configurado (se necessário)
* `SESSION_COOKIE_SECURE = True`
* `CSRF_COOKIE_SECURE = True`
* `SECURE_SSL_REDIRECT = True`
* `SECURE_HSTS_SECONDS` definido
* Arquivos estáticos **não** servidos pelo Django
* Logs de erro configurados

---

# ⚙️ Settings obrigatórios explicados

## DEBUG

```python
DEBUG = False
```

Com `DEBUG = True` em produção:

* Traceback completo exposto ao usuário
* Informações internas do sistema visíveis
* Risco crítico

---

## SECRET_KEY

```python
SECRET_KEY = os.environ.get("SECRET_KEY")
```

Usado pelo Django para:

* Assinar cookies
* Proteger sessões
* Gerar tokens CSRF

Se exposto ou previsível, toda segurança baseada em sessão é comprometida.

---

## ALLOWED_HOSTS

```python
ALLOWED_HOSTS = os.environ.get("ALLOWED_HOSTS", "").split(",")
```

Sem isso, Django aceita qualquer `Host` header.
Protege contra ataques de HTTP Host Header Injection.

---

## CSRF

```python
CSRF_COOKIE_SECURE = True
CSRF_TRUSTED_ORIGINS = ["https://meudominio.com"]
```

`CSRF_COOKIE_SECURE` garante que o cookie só trafega via HTTPS.
`CSRF_TRUSTED_ORIGINS` obrigatório quando há proxy ou domínio customizado.

---

## Sessão

```python
SESSION_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True
```

* `SECURE` → cookie só via HTTPS
* `HTTPONLY` → cookie inacessível via JavaScript

---

## HTTPS

```python
SECURE_SSL_REDIRECT = True
SECURE_HSTS_SECONDS = 31536000  # 1 ano
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True
```

`SECURE_SSL_REDIRECT` redireciona todo HTTP para HTTPS.

`HSTS` instrui o browser a **sempre** usar HTTPS para o domínio.

⚠️ Atenção com `HSTS`:
* Uma vez ativado, não é fácil reverter
* Testar em staging antes de produção
* `PRELOAD` submete o domínio à lista global de preload — decisão permanente

---

## Headers adicionais

```python
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = "DENY"
```

* `NOSNIFF` → impede browser de inferir tipo de conteúdo
* `X_FRAME_OPTIONS` → protege contra clickjacking

---

# 🗂 Settings de produção — exemplo consolidado

```python
# config/settings/prod.py

import os

DEBUG = False

SECRET_KEY = os.environ.get("SECRET_KEY")

ALLOWED_HOSTS = os.environ.get("ALLOWED_HOSTS", "").split(",")

CSRF_COOKIE_SECURE = True
CSRF_TRUSTED_ORIGINS = os.environ.get("CSRF_TRUSTED_ORIGINS", "").split(",")

SESSION_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True

SECURE_SSL_REDIRECT = True
SECURE_HSTS_SECONDS = 31536000
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True

SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = "DENY"
```

---

# 🧪 Como verificar em produção

O Django tem um comando built-in de verificação:
python manage.py check --deploy

Ele aponta configurações inseguras para ambiente de produção.
Rodar antes de qualquer deploy.

---

# 🚫 Anti-padrões

Evitar:

* `DEBUG = True` em produção
* `ALLOWED_HOSTS = ["*"]`
* `SECRET_KEY` hardcoded
* Ignorar output do `manage.py check --deploy`
* Copiar settings de dev para prod sem revisão
* Desabilitar CSRF sem justificativa registrada

---

# 🗂 Fonte da Verdade

* `config/settings/prod.py` é fonte primária
* Variáveis de ambiente definem valores reais
* ADR registra decisões estruturais relevantes

Se comportamento em produção divergir do esperado:

1. Verificar variáveis de ambiente ativas
2. Rodar `manage.py check --deploy`
3. Revisar settings carregados

---

# 📚 Relação com outros documentos

* `security/secrets.md` — gestão de segredos e variáveis de ambiente
* `django/settings.md` — organização de settings por ambiente
* `docker/compose.md` — variáveis de ambiente no container

---

# 📌 Nota final

Django oferece as ferramentas.
Segurança em produção é decisão de quem configura.

`manage.py check --deploy` antes de todo deploy.
Sem exceção.
