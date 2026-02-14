# DDD — Domain-Driven Design (Uso Prático)

Este documento descreve **como aplico Domain-Driven Design (DDD)** na prática.

Não implemento DDD “acadêmico completo”.
Uso seus conceitos para:

* Modelar melhor o domínio
* Proteger regras de negócio
* Melhorar comunicação técnica
* Reduzir acoplamento acidental
* Sustentar crescimento do sistema

DDD aqui é **ferramenta de clareza**, não dogma.

---

# 🎯 Quando aplico DDD

Aplico DDD quando:

* O domínio é relevante
* Existem regras não triviais
* Estados e transições importam
* O sistema tende a evoluir

Se é apenas CRUD simples, não forço DDD completo.

---

# 🧠 Princípios fundamentais que sigo

## 🔤 Linguagem Ubíqua

O código deve usar **a mesma linguagem do negócio**.

Isso vale para:

* Nomes de classes
* Métodos
* Atributos
* Documentação
* ADRs

Se o nome não faz sentido fora do código, o modelo provavelmente está errado.

---

## 🏛 Domínio no centro

O domínio:

* Expressa regras
* Garante invariantes
* Define estados válidos
* Representa conceitos reais

Ele **não conhece**:

* Banco de dados
* Framework
* HTTP
* Filas
* ORM

Persistência é detalhe.

---

## 🧱 Modelagem antes de persistência

Ordem mental correta:

1. Quais são os conceitos?
2. Quais regras existem?
3. Quais estados são válidos?
4. O que pode mudar?
5. O que deve ser protegido?

Só depois penso em:

* Como salvar
* Como expor
* Como integrar

---

# 🧩 Blocos estruturais do domínio

## 1️⃣ Entidades

Usadas quando:

* Identidade importa
* Estado muda ao longo do tempo

Características:

* Possuem ID
* Contêm comportamento
* Garantem invariantes

Evito entidades anêmicas.

---

## 2️⃣ Value Objects

Usados quando:

* Identidade não importa
* Valor define o objeto
* Devem ser imutáveis

Características:

* Sem ID
* Comparação por valor
* Encapsulam validações simples

---

## 3️⃣ Aggregates

Aggregate é um conjunto consistente de entidades
com **uma raiz de agregação**.

Regras que sigo:

* Acesso externo apenas pela raiz
* Invariantes protegidas dentro do aggregate
* Transações respeitam limite do aggregate

Se dois objetos sempre mudam juntos, provavelmente pertencem ao mesmo aggregate.

---

## 4️⃣ Repositórios

Repositórios são **interfaces**, não implementações.

Responsabilidade:

* Abstrair persistência
* Fornecer aggregates

Regras:

* Definidos no domínio ou application
* Implementados na infraestrutura
* Não retornam dicionários crus

---

# 🔁 Casos de Uso (Application Layer)

Casos de uso:

* Orquestram ações
* Coordenam domínio
* Controlam fluxo

Eles **não devem**:

* Conter regra de negócio profunda
* Conhecer detalhes de framework

Regra prática:

> Se a regra é do negócio, ela vive no domínio.

---

# 🧪 Testabilidade como indicador

DDD bem aplicado permite:

* Testes claros de regras
* Testes sem banco
* Testes legíveis (dado / quando / então)

Se testar é difícil:

* Regra está no lugar errado
* Modelo está fraco
* Aggregate está mal definido

---

# ⚖️ Trade-offs conscientes

Adotar DDD implica:

* Mais código
* Mais conceitos
* Mais disciplina

Aceito esses custos quando:

* O domínio é central
* O projeto terá longevidade

Não aplico DDD completo em projetos triviais.

---

# 🚫 Anti-padrões que evito

* Entidades anêmicas
* Regra espalhada em services genéricos
* Repositórios retornando estruturas cruas
* Usar DDD apenas como organização de pastas
* Ignorar limites de aggregate

---

# 🔄 DDD incremental

DDD cresce com entendimento do domínio.

Aplico em fases:

1. Linguagem e entidades
2. Invariantes e aggregates
3. Refinamentos (events, policies, etc.)

Não antecipo complexidade.

---

# 🗂 Fonte da Verdade

Quando DDD for aplicado em um projeto real:

* Código expressa o modelo real
* Testes validam regras e invariantes
* ADR registra decisões estruturais

Se a implementação divergir deste documento:

1. Atualizar documento
2. Ou registrar novo ADR justificando mudança

---

# 📚 Relação com outros documentos

* `architecture/clean-architecture.md`
* `architecture/decisions.md`
* `django/mvt.md`

---

# 📌 Nota final

Se o domínio não está claro,
nem Clean Architecture nem framework vão salvar o sistema.
