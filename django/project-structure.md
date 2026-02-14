# Django — Estrutura de Projeto (Uso Prático)

Este documento descreve **como estruturo projetos Django**
alinhados com Clean Architecture, DDD e o modelo de ADR definido neste handbook.

Estrutura não é estética.
É **governança estrutural**.

---

# 🎯 Objetivo da estrutura

A estrutura deve:

* Deixar claro onde cada tipo de código vive
* Evitar acoplamento acidental
* Proteger o domínio do framework
* Facilitar testes por camada
* Permitir crescimento sem reestruturações traumáticas

Se preciso "procurar" onde algo deveria estar,
a estrutura está fraca.

---

# 🧠 Princípios estruturais

* Domínio separado de framework
* Apps representam **contextos de negócio**, não camadas técnicas
* Web é borda do sistema (adapter)
* Infraestrutura é detalhe
* Dependências apontam para dentro
* Decisões estruturais relevantes geram ADR

---

# 🏗️ Estrutura base recomendada

No meu padrão atual, **`web/` é a camada Adapter (Django)**.

Os apps Django vivem dentro de `web/` (ex: `web/chamados`, `web/execucao`).

> Quando eu uso `web/` como raiz, estou explicitando que o framework é borda do sistema.

Exemplo base:

```
project/
├── manage.py
├── pyproject.toml
├── config/
│   ├── settings/
│   ├── urls.py
│   └── asgi.py
│
├── web/                    # Adapter Django (borda do sistema)
│   ├── chamados/
│   │   ├── domain/
│   │   ├── application/
│   │   ├── infrastructure/
│   │   └── web/
│   │
│   ├── execucao/
│   ├── iam/
│   └── redes/
│
├── shared/ (opcional)
│   ├── domain/
│   ├── application/
│   └── infrastructure/
│
├── tests/
└── docker/
```

Observações:

* `web/<contexto>/web/` pode ser renomeado quando fizer sentido (ex: `views/`, `urls/`, `templates/`).
* O importante é manter **a separação de camadas dentro do contexto**.

---

# 🧩 Organização por app (Contexto)

Cada app representa um **bounded context**.

Exemplos:

* `chamado`
* `cadastro`
* `execucao`

Evito:

* `utils` genérico
* `core` sem significado de negócio
* Apps puramente técnicos sem domínio claro

---

# 🧱 Estrutura interna de um app

## 1️⃣ domain/

Contém:

* Entidades
* Value Objects
* Aggregates
* Regras de negócio
* Interfaces de repositório

Não contém:

* ORM
* Django
* HTTP
* Framework

Domínio deve ser puro.

---

## 2️⃣ application/

Contém:

* Casos de uso
* Orquestração de fluxo
* Serviços de aplicação

Depende de:

* domain

Não contém:

* Implementações técnicas
* Detalhes de framework

---

## 3️⃣ infrastructure/

Contém:

* Models Django (ORM)
* Implementações concretas de repositório
* Integrações externas
* Serviços técnicos

Depende de:

* application
* domain

---

## 4️⃣ web/

Contém:

* Views
* Forms / Serializers
* URLs
* Templates

Responsabilidade:

* Adaptar HTTP para Application
* Adaptar resposta para cliente

Não contém:

* Regra de negócio
* Decisões estruturais

---

# 🔁 Mapeamento mental com MVT

* Model (Django) → infrastructure
* View → web
* Template → web/templates
* Domínio real → domain (fora do ORM)

Django é adaptado à arquitetura.
Não o contrário.

---

# 🧪 Estratégia de testes alinhada à estrutura

* domain → testes unitários puros
* application → testes de fluxo
* web → testes request/response
* infrastructure → testes de integração

Se um teste precisa atravessar todas as camadas para validar regra simples,
a separação está incorreta.

---

# ⚖️ Trade-offs conscientes

Essa estrutura implica:

* Mais pastas
* Mais arquivos
* Maior disciplina

Aceito quando:

* O domínio é relevante
* O sistema tende a crescer
* Longevidade importa

Em projetos simples, simplifico conscientemente.

---

# 🚫 Anti-padrões que evito

* Lógica de negócio em models Django
* Apps gigantes sem fronteira clara
* `services.py` genérico acumulador
* Domínio misturado com ORM
* Infra importando web

---

# 🗂 Fonte da Verdade

Em projetos reais:

* Código é fonte primária
* Testes validam comportamento
* ADR registra decisões estruturais

Documentação estrutural deve conter:

**Última revisão**
**Fonte (código, testes, ADRs relacionadas)**

Se houver divergência:

1. Código prevalece
2. Documento deve ser atualizado
3. Se estrutural, criar novo ADR

---

# 📚 Relação com outros documentos

* `django/mvt.md`
* `architecture/clean-architecture.md`
* `architecture/ddd.md`
* `architecture/decisions.md`

---

# 📌 Nota final

Se a estrutura não ajuda a decidir onde colocar código,
elas não está cumprindo seu papel.
