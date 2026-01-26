# Django — Estrutura de Projeto (Uso Prático)

Este documento descreve **como eu estruturo projetos Django**
de forma alinhada com Clean Architecture e DDD.

O objetivo é manter:
- clareza de responsabilidades
- limites explícitos entre camadas
- crescimento sustentável do projeto

Estrutura não é estética.
É **governança**.

---

## 🎯 Objetivo da estrutura

A estrutura do projeto deve:

- deixar claro onde cada tipo de código vive
- evitar acoplamento acidental
- facilitar testes
- permitir evolução sem reestruturações traumáticas

Se preciso “procurar” onde colocar algo,
a estrutura está fraca.

---

## 🧠 Princípios que guiam a estrutura

- domínio separado de framework
- apps representam **contextos**, não camadas
- web é borda do sistema
- infraestrutura é detalhe
- dependências apontam para dentro

---

## 🏗️ Visão geral da estrutura

Exemplo base:

project/
├── manage.py
├── pyproject.toml
├── config/ # Configuração do Django (settings, urls, wsgi)
│ ├── settings/
│ ├── urls.py
│ └── asgi.py
│
├── apps/
│ ├── chamado/
│ │ ├── domain/
│ │ ├── application/
│ │ ├── infrastructure/
│ │ └── web/
│ │
│ ├── cadastro/
│ └── execucao/
│
├── shared/ # Código compartilhado (opcional)
│ ├── domain/
│ ├── application/
│ └── infrastructure/
│
├── tests/
│
└── docker/


---

## 🧩 Organização por app (contexto)

Cada app representa um **contexto de negócio**,
não uma camada técnica.

Exemplo:
- `chamado`
- `cadastro`
- `execucao`

Evito:
- `utils`
- `core` genérico
- apps técnicos sem domínio claro

---

## 🧱 Estrutura interna de um app

### `domain/`

Contém:
- entidades
- value objects
- aggregates
- regras de negócio
- interfaces de repositório

Não contém:
- ORM
- Django
- HTTP
- detalhes técnicos

---

### `application/`

Contém:
- casos de uso
- serviços de aplicação
- orquestração de fluxo

Depende de:
- domain (interfaces)

Não contém:
- lógica de framework
- persistência concreta

---

### `infrastructure/`

Contém:
- models Django (ORM)
- implementações de repositórios
- integrações externas
- detalhes técnicos

Depende de:
- application
- domain

---

### `web/`

Contém:
- views
- serializers/forms
- urls
- controllers HTTP

Responsabilidade:
- entrada e saída do sistema

Não contém:
- regra de negócio
- decisões de domínio

---

## 🔁 Relação com Django (MVT)

Mapeamento mental:

- **Model (Django)** → `infrastructure`
- **View** → `web`
- **Template** → `web/templates`
- **Domínio real** → `domain` (fora do ORM)

Django é adaptado à arquitetura,
não o contrário.

---

## 🧪 Testes e estrutura

Estratégia comum:

- domínio → testes unitários
- application → testes de fluxo
- web → testes de request/response
- infraestrutura → testes de integração

Estrutura ajuda a testar **no nível certo**.

---

## ⚖️ Trade-offs aceitos

Essa estrutura implica:

- mais pastas
- mais arquivos
- onboarding inicial maior

Aceito isso quando:
- domínio é relevante
- projeto vai crescer
- regras importam

Para projetos simples,
simplifico conscientemente.

---

## 🚫 Anti-padrões comuns

Evitar:

- lógica de negócio em models Django
- apps gigantes sem fronteira
- `services.py` genérico
- domínio misturado com ORM
- infra importando web

---

## 🔄 Adaptação consciente

Nem todo projeto precisa dessa estrutura completa.

Eu adapto:
- MVP → estrutura reduzida
- sistema crítico → separação completa

A regra é:
> estrutura serve o domínio, não o ego arquitetural.

---

## 📚 Relação com outros documentos

- `django/mvt.md`
- `architecture/clean-architecture.md`
- `architecture/ddd.md`
- `architecture/decisions.md`

---

## 📌 Nota final

Se a estrutura não ajuda a decidir
onde colocar código,
ela não está cumprindo seu papel.