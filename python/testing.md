# Python — Testing (Uso Prático)

Este documento descreve **como eu abordo testes em projetos Python**.

O objetivo não é “ter 100% de cobertura”, mas:
- garantir comportamento correto
- proteger regras importantes
- permitir refatoração sem medo
- detectar erro cedo

Teste é ferramenta de **confiança**, não de vaidade.

---

## 🎯 Por que testar

Eu testo para:

- validar regras de negócio
- evitar regressões
- documentar comportamento esperado
- ganhar segurança para refatorar
- reduzir bugs em produção

Se um código é difícil de testar,
geralmente ele também é difícil de manter.

---

## 🧠 Princípios que eu sigo

- testes focam **comportamento**, não implementação
- testes devem ser legíveis
- falha de teste deve explicar o problema
- testes rápidos > testes perfeitos
- regra de negócio tem prioridade máxima

---

## 🧰 Ferramenta base

Uso **pytest** como base para testes Python.

Motivos:
- sintaxe simples
- fixtures poderosas
- ótimo ecossistema
- fácil integração com Django

---

## 🗂️ Estrutura de testes

Estrutura comum:

tests/
├── domain/
├── application/
├── web/
└── infrastructure/


A estrutura de testes reflete **a arquitetura do projeto**,
não o framework.

---

## 🧪 Tipos de teste (como eu classifico)

### Testes unitários

Foco:
- regras de negócio
- entidades
- value objects
- validações

Características:
- rápidos
- sem banco
- sem framework
- isolados

> Prioridade máxima.

---

### Testes de aplicação (casos de uso)

Foco:
- fluxo de execução
- orquestração
- chamadas corretas ao domínio

Características:
- podem usar mocks
- validam integração entre camadas internas
- não dependem de HTTP

---

### Testes de integração

Foco:
- infraestrutura real
- banco de dados
- ORM
- integrações externas (quando necessário)

Características:
- mais lentos
- mais frágeis
- usados com parcimônia

---

### Testes de web / API

Foco:
- request/response
- status codes
- payloads
- permissões

Características:
- validam borda do sistema
- não testam regra de negócio profunda
- normalmente usam client de teste

---

## 🧠 Regra de ouro

> **Se a regra é do negócio, ela deve ser testada sem Django, banco ou HTTP.**

Se um teste de regra exige:
- RequestFactory
- Client
- banco de dados

provavelmente a regra está no lugar errado.

---

## 🧪 Fixtures (uso consciente)

Uso fixtures para:
- criar dados reutilizáveis
- montar contexto de teste
- reduzir duplicação

Evito:
- fixtures mágicas
- fixtures gigantes
- fixtures que escondem comportamento

Regra prática:
> fixture deve preparar cenário, não fazer lógica.

---

## 🔀 Mocks e stubs

Uso mocks quando:
- quero isolar dependência externa
- testar apenas o comportamento do código atual

Evito:
- mockar tudo
- mockar domínio
- mockar para “forçar” teste passar

Se preciso de muitos mocks,
talvez o design esteja ruim.

---

## 🧪 Nomes e organização dos testes

Boas práticas:
- nomes claros
- estrutura `dado_quando_entao`
- um comportamento por teste

Exemplo:

```python
def test_nao_permite_finalizar_chamado_sem_itens():
    ...
Um teste deve responder:

“o que acontece quando X?”

🧪 Testes e Django
Em projetos Django:

domínio → testes unitários puros

application → testes focados em fluxo

web → django.test.Client

ORM → testes de integração

Não uso Django para testar regra que não depende dele.

🚫 Anti-padrões comuns
Evitar:

testar getters/setters

testar framework

testes gigantes que validam tudo

testes que dependem de ordem

testes frágeis por excesso de mock

ignorar testes quebrados por muito tempo

🧠 Checklist rápido
Antes de escrever ou revisar um teste:

 estou testando comportamento?

 este teste quebraria se a regra mudasse?

 ele é legível sem contexto extra?

 roda rápido?

 falha com mensagem clara?

📌 Nota final
Testes bons não impedem bugs.
Eles impedem surpresas.

Se testar virou sofrimento,
o problema raramente é o pytest.
Geralmente é o design.