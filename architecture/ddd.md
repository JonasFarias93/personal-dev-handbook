# DDD — Domain-Driven Design (Uso Prático)

Este documento descreve **como eu aplico Domain-Driven Design (DDD)** na prática.

O objetivo não é implementar DDD “completo” ou acadêmico,
mas usar seus conceitos para:
- modelar melhor o domínio
- proteger regras de negócio
- melhorar comunicação
- reduzir acoplamento acidental

DDD aqui é **ferramenta de clareza**, não dogma.

---

## 🎯 Por que usar DDD

Uso DDD quando:

- o domínio é relevante
- regras de negócio são complexas
- decisões importam mais do que CRUD
- o sistema tende a crescer

DDD ajuda a responder:
> “O que realmente importa neste sistema?”

---

## 🧠 Princípios que eu sigo

### Linguagem ubíqua

O código deve usar **as mesmas palavras do negócio**.

- nomes de classes, métodos e atributos
- documentação
- conversas técnicas

Se o nome não faz sentido fora do código,
provavelmente o modelo está errado.

---

### Domínio no centro

O domínio:
- expressa regras
- valida invariantes
- representa conceitos reais

Ele **não conhece**:
- banco de dados
- framework
- transporte (HTTP, fila, etc.)

---

### Modelagem antes de persistência

Primeiro eu penso:
- quais são os conceitos?
- quais regras existem?
- quais estados são válidos?

Depois eu penso:
- como salvar isso
- como expor isso

Persistência é detalhe.

---

## 🧱 Blocos principais do domínio

### Entidades

Usadas quando:
- identidade importa
- o objeto muda ao longo do tempo

Características:
- possuem ID
- possuem comportamento
- garantem invariantes

Exemplo:
- Chamado
- Pedido
- Usuário

---

### Value Objects

Usados quando:
- identidade não importa
- valor define o objeto
- são imutáveis

Características:
- não possuem ID
- são comparados por valor
- encapsulam validações simples

Exemplo:
- Status
- Endereço
- Intervalo de datas

---

### Aggregates

Um **Aggregate** é um conjunto consistente de entidades
com **uma raiz de agregação**.

Regras:
- acesso externo acontece apenas pela raiz
- invariantes são protegidas dentro do aggregate
- transações respeitam limites do aggregate

Exemplo:
- Chamado (raiz) → Itens, Status, Histórico

---

### Repositórios

Repositórios são **interfaces**, não implementações.

Responsabilidade:
- abstrair persistência
- fornecer coleções de aggregates

Regras:
- definidos no domínio ou application
- implementados na infraestrutura
- retornam aggregates, não registros crus

---

## 🔁 Casos de uso (Application Layer)

Casos de uso:
- coordenam ações
- chamam domínio
- orquestram dependências

Eles **não**:
- contêm regra de negócio profunda
- sabem detalhes de framework
- fazem validação complexa de domínio

Regra prática:
> Se a regra é do negócio, ela vive no domínio.

---

## 🧪 Testabilidade

DDD facilita:

- testes focados em regras
- testes sem banco
- testes legíveis (“dado / quando / então”)

Se testar é difícil:
- regra está no lugar errado
- modelo está fraco

---

## ⚖️ Trade-offs aceitos

Adotar DDD implica:

- mais código
- mais conceitos
- curva de aprendizado maior

Aceito esses custos quando:
- domínio justifica
- longevidade do projeto importa

Para CRUD simples, **não forço DDD**.

---

## 🚫 Anti-padrões comuns

Evitar:

- entidades anêmicas
- domínio só com getters/setters
- regras espalhadas em services
- repositórios retornando dicionários
- usar DDD só como “nome bonito de pasta”

---

## 🔄 DDD incremental

DDD não precisa nascer completo.

Eu aplico:
- primeiro: linguagem e entidades
- depois: invariantes e aggregates
- por último: refinamentos (events, policies, etc.)

DDD cresce junto com o entendimento do domínio.

---

## 📚 Relação com outros documentos

- `architecture/clean-architecture.md` — organização do sistema
- `architecture/decisions.md` — decisões arquiteturais
- `django/mvt.md` — adaptação ao Django

---

## 📌 Nota final

Se o domínio não está claro,
nenhuma arquitetura vai salvar o sistema.