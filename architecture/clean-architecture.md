# Clean Architecture — Uso Prático

Este documento descreve **como eu aplico Clean Architecture na prática**.

O objetivo não é seguir o modelo “puro” de livros,
mas usar seus princípios para construir sistemas:
- mais fáceis de entender
- mais fáceis de testar
- mais fáceis de evoluir

---

## 🎯 Por que Clean Architecture

Adoto Clean Architecture para:

- proteger regras de negócio
- reduzir acoplamento com frameworks
- facilitar testes
- permitir evolução sem reescrever tudo
- manter decisões explícitas

Não é sobre pastas.
É sobre **direção de dependência**.

---

## 🧠 Princípios fundamentais

### Dependências apontam para dentro

Código mais externo pode depender do interno.  
O interno **nunca** depende do externo.

- domínio não depende de framework
- regras de negócio não conhecem banco, web ou UI
- detalhes mudam, regras não

---

### Regras de negócio no centro

O domínio:
- contém regras
- contém invariantes
- contém linguagem do problema

Ele não sabe:
- como dados são persistidos
- como requests chegam
- como respostas são entregues

---

### Frameworks são detalhes

Frameworks (Django, FastAPI, ORM, etc):
- facilitam implementação
- **não definem o domínio**

Se o framework mudar, o domínio deve sobreviver.

---

## 🏗️ Camadas (visão prática)

### Domain

**Responsabilidade**
- regras de negócio
- entidades
- value objects
- validações
- invariantes

**Não pode**
- importar ORM
- importar web
- acessar banco
- conhecer framework

---

### Application (ou Use Cases)

**Responsabilidade**
- orquestrar regras
- coordenar casos de uso
- definir fluxo da aplicação

**Pode**
- chamar domínio
- depender de interfaces (ports)

**Não pode**
- acessar detalhes concretos
- conter lógica de framework

---

### Infrastructure

**Responsabilidade**
- implementar detalhes técnicos
- persistência
- integrações
- serviços externos

**Depende de**
- application
- domain (interfaces)

---

### Interface / Web

**Responsabilidade**
- entrada e saída do sistema
- tradução de dados (DTOs, serializers)
- validação superficial de input

**Não deve**
- conter regra de negócio
- decidir fluxo complexo

---

## 🔁 Fluxo típico

1. Request entra pela camada Web
2. Web traduz input → chama Application
3. Application executa caso de uso
4. Domain valida regras e invariantes
5. Infrastructure fornece dados / persiste
6. Resultado volta em sentido inverso

> O domínio nunca “sobe” camadas.

---

## 🧪 Testabilidade

Essa arquitetura permite:

- testar domínio sem banco
- testar casos de uso sem framework
- testar infraestrutura isoladamente

Regra prática:
> Se é difícil testar, provavelmente está acoplado demais.

---

## ⚖️ Trade-offs aceitos

Adotar Clean Architecture implica:

- mais arquivos
- mais camadas
- mais código “cerimonial”

Esses custos são aceitos quando:
- o domínio é relevante
- o sistema tende a crescer
- regras de negócio importam

Em projetos muito simples, **não aplico tudo**.

---

## 🚫 Anti-padrões comuns

Evitar:

- domínio importando ORM
- services “faz-tudo”
- lógica de negócio em views
- regras escondidas em signals/hooks
- “camadas” que só repassam dados

---

## 🔄 Adaptação consciente

Clean Architecture **não é binária**.

Eu aplico:
- o suficiente para proteger o domínio
- sem criar abstrações prematuras
- adaptando ao tamanho do projeto

Arquitetura serve o sistema.
Não o contrário.

---

## 📚 Relação com outros documentos

- `architecture/ddd.md` — modelagem do domínio
- `architecture/decisions.md` — decisões arquiteturais
- `django/mvt.md` — adaptação ao Django

---

## 📌 Nota final

Se a arquitetura não ajuda a entender o sistema,
ela está falhando.
