# Python — Testing (Uso Prático)

Este documento descreve **como abordo testes em projetos Python**,
alinhado com Clean Architecture, DDD e governança de qualidade.

Teste é ferramenta de confiança.
Não é métrica de vaidade.

---

# 🎯 Por que testar

Eu testo para:

* Validar regras de negócio
* Evitar regressões
* Documentar comportamento esperado
* Permitir refatoração segura
* Detectar erro cedo

Se um código é difícil de testar,
provavelmente é difícil de manter.

---

# 🧠 Princípios que sigo

* Testes focam comportamento, não implementação
* Testes devem ser legíveis
* Falha deve explicar o problema
* Testes rápidos > testes excessivamente complexos
* Regras de negócio têm prioridade máxima
* Arquitetura orienta a estratégia de teste

---

# 🧰 Ferramenta base

Uso **pytest** como base padrão.

Motivos:

* Sintaxe simples
* Fixtures poderosas
* Ecossistema maduro
* Integração natural com Django

Configuração centralizada no `pyproject.toml`.

---

# 🗂 Estrutura de testes

A estrutura reflete a arquitetura do projeto:

```
tests/
├── domain/
├── application/
├── web/
└── infrastructure/
```

Testes seguem as camadas.
Não seguem o framework.

---

# 🧪 Tipos de teste

## 1️⃣ Testes unitários (Domínio)

Foco:

* Entidades
* Value Objects
* Invariantes
* Regras de negócio

Características:

* Rápidos
* Sem banco
* Sem framework
* Isolados

> Prioridade máxima.

---

## 2️⃣ Testes de aplicação (Use Cases)

Foco:

* Fluxo de execução
* Orquestração
* Chamadas corretas ao domínio

Características:

* Podem usar mocks controlados
* Não dependem de HTTP

---

## 3️⃣ Testes de integração (Infraestrutura)

Foco:

* ORM
* Banco de dados
* Implementações concretas

Características:

* Mais lentos
* Usados com parcimônia
* Validam comportamento real

---

## 4️⃣ Testes de Web / API

Foco:

* Request/Response
* Status codes
* Permissões
* Serialização

Não testam regra profunda.
Apenas a borda.

---

# 🧠 Regra de ouro

> Se a regra é do negócio, ela deve ser testada sem Django, banco ou HTTP.

Se o teste exige `Client`, banco ou RequestFactory para validar regra pura,
o design está incorreto.

---

# 🧩 Fixtures (uso consciente)

Uso fixtures para:

* Criar dados reutilizáveis
* Montar contexto
* Reduzir duplicação

Evito:

* Fixtures mágicas
* Fixtures gigantes
* Lógica escondida em fixture

Fixture prepara cenário.
Não executa regra.

---

# 🔀 Mocks e Stubs

Uso mocks quando:

* Quero isolar dependência externa
* Testo comportamento da unidade atual

Evito:

* Mockar domínio
* Mockar tudo indiscriminadamente
* Mockar para "forçar" teste passar

Muitos mocks geralmente indicam design frágil.

---

# 🧪 Padrão de escrita

Boas práticas:

* Um comportamento por teste
* Nome claro e explícito
* Estrutura dado → quando → então

Exemplo:

```python
def test_nao_permite_finalizar_chamado_sem_itens():
    ...
```

Um teste deve responder:

> O que acontece quando X?

---

# 🧪 Testes e Django

Em projetos Django:

* Domínio → testes unitários puros
* Application → testes de fluxo
* Web → `django.test.Client`
* ORM → integração real

Não uso Django para testar regra que não depende dele.

---

# 🔄 Relação com DoD

Mudança de comportamento só está pronta quando:

* Teste cobre o cenário principal
* Cenário negativo foi considerado
* Testes existentes continuam passando

Se a mudança quebra teste inesperadamente,
verificar se foi regressão ou regra mudou.

---

# 🚫 Anti-padrões

Evitar:

* Testar getters/setters
* Testar comportamento interno irrelevante
* Testes gigantes validando tudo
* Dependência de ordem de execução
* Ignorar teste quebrado por tempo prolongado

---

# 🧠 Checklist rápido

Antes de considerar um teste adequado:

* Estou testando comportamento real?
* O teste falharia se a regra mudasse?
* É legível sem contexto adicional?
* Roda rápido?
* Mensagem de falha é clara?

---

# 🗂 Fonte da Verdade

* Código implementa comportamento
* Testes validam comportamento
* `pyproject.toml` define tooling
* DoD exige testes quando aplicável
* ADR registra mudanças estruturais

Se teste e código divergem:

1. Verificar qual representa a regra correta
2. Ajustar o incorreto

---

# 📌 Nota final

Testes não impedem bugs.
Eles impedem surpresas.

Se testar virou sofrimento,
provavelmente o problema é o design,
não o pytest.
