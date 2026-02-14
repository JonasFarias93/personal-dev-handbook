# Django — Settings (Uso Prático)

Este documento define **como organizo e configuro settings em projetos Django**,
alinhado com Clean Architecture, separação por ambientes e governança formal.

Settings são parte da arquitetura.
Mudanças relevantes podem exigir ADR.

---

# 🎯 Objetivo dos settings

Settings devem:

* Ser previsíveis entre ambientes (dev / test / prod)
* Tornar explícito o que muda por ambiente
* Manter segredos fora do repositório
* Reduzir risco operacional
* Evitar comportamento implícito

---

# 🧠 Princípios que sigo

* Segredo nunca entra no Git
* Ambientes são explícitos
* Configuração vem do ambiente (env vars)
* Defaults seguros (especialmente em produção)
* Arquivos pequenos e organizados
* Mudanças estruturais relevantes geram ADR

---

# 🗂 Organização recomendada

Uso separação por ambiente.

```
config/
└── settings/
    ├── __init__.py
    ├── base.py
    ├── dev.py
    ├── prod.py
    └── test.py
```

## base.py

Contém o comum entre ambientes:

* INSTALLED_APPS base
* MIDDLEWARE base
* Templates
* Timezone / Language
* Static / Media base
* Logging base

Não contém segredo.

---

## dev.py

Ambiente local:

* DEBUG = True
* Email backend de console
* DB local
* Ferramentas de debug (quando necessário)

Facilita desenvolvimento, mas com consciência de risco.

---

## prod.py

Produção:

* DEBUG = False
* ALLOWED_HOSTS obrigatório
* SECRET_KEY via env
* DB via env
* Cookies seguros
* Headers avaliados
* Logging robusto

Produção deve ser explícita e segura.

---

## test.py

Testes priorizam:

* Isolamento
* Previsibilidade
* Velocidade

Decisões comuns:

* Email backend em memória
* Cache simplificado
* Remoção de integrações externas

---

# 🔐 Variáveis de ambiente (Source of Configuration)

Tudo que for:

* Segredo
* Dependente de ambiente
* Integração externa

Deve vir via env.

Exemplos comuns:

* SECRET_KEY
* DATABASE_URL
* DEBUG
* ALLOWED_HOSTS
* CSRF_TRUSTED_ORIGINS
* EMAIL_*
* SENTRY_DSN

Regra prática:

> Se eu não posso publicar isso, vai para env.

---

# 🧭 Seleção do settings ativo

Seleciono via variável de ambiente:

```
DJANGO_SETTINGS_MODULE=config.settings.dev
DJANGO_SETTINGS_MODULE=config.settings.prod
```

Evito:

* if/else gigante dentro de um único arquivo
* lógica complexa condicional baseada em DEBUG

---

# ✅ Regras mínimas de segurança (produção)

Em produção, revisar explicitamente:

* DEBUG = False
* SECRET_KEY via env
* ALLOWED_HOSTS definido
* CSRF_TRUSTED_ORIGINS (se necessário)
* SESSION_COOKIE_SECURE
* CSRF_COOKIE_SECURE
* SECURE_SSL_REDIRECT (se aplicável)
* Headers de segurança

Não confiar cegamente nos defaults do Django.

---

# 📦 Static / Media

Definir claramente:

* STATIC_URL
* STATIC_ROOT
* MEDIA_URL
* MEDIA_ROOT

Em produção:

* Django não deve servir arquivos estáticos diretamente
* Infra (Nginx/CDN/Storage) deve assumir essa responsabilidade

---

# 🧾 Logging (mínimo viável)

* Dev → logging legível no console
* Prod → logs consistentes e rastreáveis
* Erros críticos devem ser capturáveis (ex: Sentry)

Evitar:

* Logs silenciosos em produção
* Log excessivo sem utilidade

---

# 🚫 Anti-padrões comuns

Evitar:

* Um único settings.py gigantesco
* Segredos no repositório
* Lógica complexa dentro de settings
* "Corrigir prod" com gambiarra em settings
* Comportamento implícito por ambiente

---

# 🗂 Fonte da Verdade

* Código é fonte primária
* Ambiente define configuração
* Testes garantem previsibilidade
* ADR registra decisões estruturais relevantes

Documentação de settings deve conter:

* Última revisão
* Fonte (arquivos reais, env necessários, ADR relacionada)

Se houver divergência entre documento e código:

1. Código prevalece
2. Documento deve ser atualizado
3. Se estrutural, registrar novo ADR

---

# 📚 Relação com outros documentos

* `django/project-structure.md`
* `architecture/decisions.md`
* `docker/compose.md`
* `python/pyproject.md`

---

# 📌 Nota final

Settings bons não são os "perfeitos".
São os que evitam surpresa, reduzem risco e tornam ambientes previsíveis.
