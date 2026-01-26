# Django — MVT (Uso Prático)

Este documento descreve **como eu utilizo o padrão MVT do Django**
(Model–View–Template) de forma consciente.

O objetivo não é seguir o MVT “puro”, mas **adaptá-lo**
para manter:
- regras de negócio protegidas
- domínio independente
- views simples e previsíveis

Django é ferramenta.
Arquitetura é decisão.

---

## 🎯 Papel do MVT no Django

No Django, o MVT organiza **entrada, processamento e saída**:

- **Model** → persistência e mapeamento de dados
- **View** → entrada/saída (HTTP)
- **Template** → apresentação

Importante:
> No Django, *Views não são Controllers clássicos*  
> Elas fazem **orquestração de request/response**.

---

## 🧠 Princípio central

> **Views não contêm regra de negócio.**

Views:
- recebem input
- validam superficialmente
- chamam casos de uso
- retornam resposta

Regra de negócio vive:
- no domínio
- ou na camada de aplicação

---

## 🧱 Como eu interpreto cada camada

### Model (Django ORM)

Uso os Models principalmente como:

- mapeamento para banco
- persistência de estado
- infraestrutura

**Evito:**
- regra de negócio complexa no model
- lógica de fluxo
- decisões de domínio profundas

Regra prática:
> Model ≠ Domínio (na maioria dos projetos)

Quando necessário, Models podem:
- delegar para objetos de domínio
- converter para aggregates

---

### View

Views são **finas**.

Responsabilidades:
- receber request
- validar formato e permissões
- chamar caso de uso
- traduzir resposta (HTTP, template, JSON)

Views **não devem**:
- decidir regras
- conter ifs complexos de negócio
- manipular estado diretamente

---

### Template

Templates são **burros por design**.

Responsabilidades:
- exibir dados
- loops simples
- condições básicas de apresentação

Nunca coloco:
- regra de negócio
- cálculos importantes
- decisões de fluxo

Se ficou complexo:
> lógica está no lugar errado.

---

## 🔁 Fluxo típico (request → domínio)

1. Request chega na View
2. View valida input básico (form/serializer)
3. View chama caso de uso (Application)
4. Caso de uso executa domínio
5. Resultado volta para a View
6. View responde (template / JSON / redirect)

> O domínio nunca conhece HTTP.

---

## 🧩 Forms e Serializers

Forms/Serializers:
- validam **entrada**
- não validam **regra de negócio**

Exemplos:
- tipo errado
- campo obrigatório
- formato inválido

Regras reais:
- vivem no domínio
- vivem nos casos de uso

---

## 🧪 Testes no contexto MVT

- Views → testes de integração (request/response)
- Domínio → testes unitários
- Casos de uso → testes focados em fluxo

Se testar uma regra exige RequestFactory:
> algo está errado.

---

## ⚖️ Trade-offs aceitos

Usar Django dessa forma implica:

- duplicação ocasional de validação
- mais camadas
- menos “mágica” do framework

Aceito isso em troca de:
- clareza
- previsibilidade
- domínio saudável

---

## 🚫 Anti-padrões comuns em Django

Evitar:

- lógica de negócio em views
- models “faz-tudo”
- templates com lógica complexa
- signals para regras críticas
- usar ORM como se fosse domínio

---

## 🔄 Adaptação consciente

Nem todo projeto precisa do mesmo rigor.

Eu adapto:
- projetos pequenos → menos camadas
- projetos complexos → separação clara

A regra é:
> Django se adapta ao domínio, não o contrário.

---

## 📚 Relação com outros documentos

- `architecture/clean-architecture.md`
- `architecture/ddd.md`
- `django/project-structure.md`
- `architecture/decisions.md`

---

## 📌 Nota final

Se a View ficou difícil de entender,
o problema não é o Django.
É a arquitetura.
