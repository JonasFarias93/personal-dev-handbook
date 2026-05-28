# Observabilidade — Logs e Erros

Este documento define **como estruturo logging e captura de erros**
em projetos Django.

Observabilidade não é luxo.
É o que permite entender o que acontece em produção.

---

# 🎯 Objetivo

* Tornar erros visíveis antes que o usuário reporte
* Ter contexto suficiente para diagnosticar problemas
* Estabelecer padrão mínimo desde o início do projeto

---

# 🧠 Princípio central

> Se não está logado, não existe para o desenvolvedor.

Erro silencioso em produção é pior que ausência de feature.

---

# 🗂 Níveis de log — referência rápida

| Nível | Quando usar |
|---|---|
| `DEBUG` | Detalhes internos — apenas em desenvolvimento |
| `INFO` | Eventos esperados — fluxo normal |
| `WARNING` | Algo inesperado, mas sistema segue funcionando |
| `ERROR` | Falha real — requer atenção |
| `CRITICAL` | Falha grave — sistema comprometido |

Regra prática:

* Dev → `DEBUG` e acima
* Produção → `INFO` e acima (nunca `DEBUG`)

---

# ⚙️ Configuração base de logging no Django

Adicionar em `config/settings/base.py`:

```python
LOGGING = {
    "version": 1,
    "disable_existing_loggers": False,
    "formatters": {
        "verbose": {
            "format": "{levelname} {asctime} {module} {message}",
            "style": "{",
        },
        "simple": {
            "format": "{levelname} {message}",
            "style": "{",
        },
    },
    "handlers": {
        "console": {
            "class": "logging.StreamHandler",
            "formatter": "verbose",
        },
    },
    "root": {
        "handlers": ["console"],
        "level": "INFO",
    },
    "loggers": {
        "django": {
            "handlers": ["console"],
            "level": "INFO",
            "propagate": False,
        },
    },
}
```

---

# 🔧 Ajuste por ambiente

## dev.py

```python
LOGGING["root"]["level"] = "DEBUG"
```

## prod.py

```python
LOGGING["root"]["level"] = "INFO"
```

Nunca usar `DEBUG` em produção — expõe dados internos e polui logs.

---

# 🐍 Como usar logging no código

```python
import logging

logger = logging.getLogger(__name__)

# Fluxo normal
logger.info("Chamado %s finalizado", chamado.id)

# Algo inesperado mas recuperável
logger.warning("Tentativa de finalizar chamado sem itens: %s", chamado.id)

# Erro real
logger.error("Falha ao persistir chamado: %s", str(e))

# Com traceback completo
logger.exception("Erro inesperado ao processar chamado")
```

Regra:

* `logger.exception()` captura o traceback automaticamente
* Usar `__name__` como nome do logger — identifica exatamente onde o log foi gerado
* Nunca usar `print()` para logging em produção

---

# 🐳 Relação com Docker

Com Docker, logs vão para `stdout/stderr` por padrão.

Visualizar:
docker compose logs -f web

Isso é suficiente para desenvolvimento local.
Em produção, o orquestrador (ex: Railway, Render, AWS) captura esse output.

---

# 📡 Próximo passo — Sentry

Quando o projeto for para produção, adicionar **Sentry** para captura de erros.

O que o Sentry oferece além do logging:

* Agrupamento de erros por tipo
* Stacktrace completo com contexto
* Alertas automáticos
* Histórico de ocorrências

Instalação mínima:
uv add sentry-sdk

Configuração em `prod.py`:

```python
import sentry_sdk

sentry_sdk.init(
    dsn=os.environ.get("SENTRY_DSN"),
    traces_sample_rate=0.1,
)
```

`SENTRY_DSN` via variável de ambiente — nunca hardcoded.

Decisão de adotar Sentry deve gerar ADR.

---

# ✅ Checklist mínimo por ambiente

**Desenvolvimento:**
* Logging em `DEBUG`
* Erros visíveis no console
* `print()` substituído por `logger`

**Produção:**
* Logging em `INFO`
* Erros críticos capturáveis
* Sentry configurado (quando aplicável)
* `SENTRY_DSN` via variável de ambiente

---

# 🚫 Anti-padrões

Evitar:

* `print()` como logging
* `DEBUG` ativo em produção
* Capturar exceção e silenciar sem log
* Logger genérico sem `__name__`
* Ignorar warnings por tempo prolongado

Exemplo de anti-padrão comum:

```python
# Errado — erro silencioso
try:
    finalizar_chamado(chamado)
except Exception:
    pass

# Correto
try:
    finalizar_chamado(chamado)
except Exception as e:
    logger.exception("Erro ao finalizar chamado %s", chamado.id)
    raise
```

---

# 🗂 Fonte da Verdade

* `config/settings/base.py` define logging base
* Ambiente ajusta nível via `dev.py` / `prod.py`
* `SENTRY_DSN` via variável de ambiente
* ADR registra decisão de adotar ferramenta externa

---

# 📚 Relação com outros documentos

* `security/secrets.md` — `SENTRY_DSN` é segredo
* `django/settings.md` — organização de settings por ambiente
* `docker/debugging.md` — debugging local com logs de container

---

# 📌 Nota final

Logging básico tem custo zero.
Não ter logging em produção tem custo alto.

Começar simples.
Evoluir para Sentry quando o projeto justificar.
