# Clean Architecture — Uso Prático

Este documento descreve **como aplico Clean Architecture na prática**.

Não sigo o modelo “acadêmico puro”.
Uso seus princípios para construir sistemas:

* mais fáceis de entender
* mais fáceis de testar
* mais fáceis de evoluir
* menos dependentes de frameworks

Arquitetura é ferramenta. Não dogma.

---

# 🎯 Objetivo real ao aplicar Clean Architecture

Adoto Clean Architecture quando preciso:

* Proteger regras de negócio
* Reduzir acoplamento estrutural
* Tornar testes simples
* Permitir evolução sem reescrita massiva
* Tornar decisões explícitas

Não é sobre pastas.
É sobre **direção de dependência**.

---

# 🧠 Princípio Fundamental

> Dependências sempre apontam para dentro.

Código mais externo pode depender do interno.
O interno **nunca depende do externo**.

---

# 🏛 Camadas (modelo prático que aplico)

## 1️⃣ Domain

### Responsabilidade

* Regras de negócio
* Entidades
* Value Objects
* Invariantes
* Linguagem do domínio

### Não pode

* Importar ORM
* Importar framework
* Conhecer banco de dados
* Conhecer camada web

O domínio deve sobreviver se o framework for trocado.

---

## 2️⃣ Application (Use Cases)

### Responsabilidade

* Orquestrar fluxo
* Executar casos de uso
* Coordenar domínio
* Definir contratos (interfaces/ports)

### Pode

* Chamar domínio
* Depender de interfaces

### Não pode

* Conter regra de framework
* Conhecer detalhes técnicos concretos

---

## 3️⃣ Infrastructure

### Responsabilidade

* Implementar detalhes técnicos
* Persistência
* Integrações externas
* Serviços de terceiros

Depende de:

* Domain (interfaces)
* Application

---

## 4️⃣ Interface / Web (Adapter)

### Responsabilidade

* Entrada e saída do sistema
* Tradução de dados (DTOs, serializers, forms)
* Validação superficial de input

### Não deve

* Conter regra de negócio
* Decidir fluxo complexo

Framework é detalhe.

---

# 🔁 Fluxo típico

1. Request entra pela camada Web
2. Web traduz input e chama Application
3. Application executa caso de uso
4. Domain valida regras e invariantes
5. Infrastructure persiste ou integra
6. Resultado retorna no sentido inverso

O domínio nunca “sobe” camadas.

---

# 🧪 Testabilidade como métrica

Arquitetura correta facilita testes:

* Domínio testado sem banco
* Use cases testados sem framework
* Infra testada isoladamente

Regra prática:

> Se é difícil testar, provavelmente está acoplado demais.

---

# ⚖️ Quando aplicar (e quando não aplicar)

Clean Architecture tem custo:

* Mais arquivos
* Mais abstrações
* Mais código estrutural

Aplico quando:

* O domínio é relevante
* O sistema tende a crescer
* Regras de negócio são centrais

Não aplico completamente quando:

* Projeto é simples
* Domínio é trivial
* Complexidade não se justifica

Arquitetura deve ser proporcional ao problema.

---

# 🚫 Anti-padrões que evito

* Domínio importando ORM
* Lógica de negócio em views
* Services “faz-tudo” sem responsabilidade clara
* Regras escondidas em signals/hooks
* Camadas que só repassam dados sem agregar valor

---

# 🧩 Adaptação consciente

Clean Architecture **não é binária**.

Aplico:

* O suficiente para proteger o domínio
* Sem criar abstrações prematuras
* Adaptando ao tamanho do projeto

Arquitetura serve o sistema.
Não o contrário.

---

# 🗂 Fonte da Verdade

Quando este modelo for aplicado em um projeto real:

* Código é a fonte primária
* Testes validam comportamento
* ADR registra decisão estrutural

Se a implementação divergir do documento:

1. Atualizar documento
2. Ou registrar novo ADR explicando mudança

---

# 📚 Relação com outros documentos

* `architecture/ddd.md`
* `architecture/decisions.md`
* `django/mvt.md`

---

# 📌 Nota final

Se a arquitetura não ajuda a entender o sistema,
elas está falhando.
