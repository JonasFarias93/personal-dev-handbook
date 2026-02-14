# Django — MVT (Uso Prático)

Este documento descreve **como utilizo o padrão MVT do Django**
(Model–View–Template) de forma consciente e alinhada com Clean Architecture e DDD.

O objetivo não é seguir o MVT “puro”, mas adaptá-lo para manter:

* Domínio protegido
* Views simples e previsíveis
* Framework como detalhe
* Regras de negócio fora do HTTP

Django é ferramenta.
Arquitetura é decisão.

---

# 🎯 Papel do MVT no meu modelo

No Django, o MVT organiza entrada, processamento e saída:

* **Model** → persistência (infraestrutura)
* **View** → adapter HTTP
* **Template** → apresentação

Importante:

> Views não são Controllers clássicos.
> Elas são adaptadores entre HTTP e Application.

---

# 🧠 Princípio central

> Views não contêm regra de negócio.

Views:

* Recebem input
* Validam formato
* Validam permissões
* Chamam caso de uso
* Retornam resposta

Regra de negócio vive:

* No domínio
* Ou na camada de aplicação

---

# 🧱 Como interpreto cada camada

## 1️⃣ Model (Django ORM)

Uso Models principalmente como:

* Mapeamento para banco
* Persistência de estado
* Infraestrutura técnica

Evito:

* Lógica de domínio profunda
* Regras complexas de negócio
* Decisões de fluxo

Regra prática:

> Model ≠ Domínio (na maioria dos projetos).

Quando necessário, Models podem:

* Converter para objetos de domínio
* Delegar comportamento

---

## 2️⃣ View

Views são finas.

Responsabilidades:

* Receber request
* Validar formato
* Checar autorização
* Chamar caso de uso
* Traduzir resposta (HTML, JSON, redirect)

Não devem:

* Decidir regra de negócio
* Manipular invariantes
* Conter fluxo complexo

Se a view está grande, algo está no lugar errado.

---

## 3️⃣ Template

Templates são deliberadamente simples.

Responsabilidades:

* Exibir dados
* Loops simples
* Condições de apresentação

Nunca coloco:

* Regra de negócio
* Cálculos importantes
* Decisão estrutural

Se ficou complexo:

> A lógica está no lugar errado.

---

# 🔁 Fluxo típico (HTTP → Domínio)

1. Request chega na View
2. View valida input superficial
3. View chama caso de uso (Application)
4. Caso de uso executa domínio
5. Infraestrutura persiste
6. Resultado volta para View
7. View responde

O domínio nunca conhece HTTP.

---

# 🧩 Forms e Serializers

Forms/Serializers validam:

* Tipo
* Presença
* Formato

Eles não validam:

* Regras profundas
* Invariantes
* Estados inválidos de negócio

Regra prática:

> Validação estrutural ≠ validação de domínio.

---

# 🧪 Estratégia de testes no contexto MVT

* Views → testes de integração (request/response)
* Application → testes focados em fluxo
* Domínio → testes unitários puros

Se testar regra exige RequestFactory:

> Camadas estão misturadas.

---

# ⚖️ Trade-offs conscientes

Usar Django dessa forma implica:

* Mais camadas
* Menos "mágica" do framework
* Eventual duplicação de validação

Aceito isso em troca de:

* Clareza estrutural
* Domínio protegido
* Evolução segura

---

# 🚫 Anti-padrões que evito

* Lógica de negócio em views
* Models “faz-tudo”
* Templates com lógica complexa
* Signals para regras críticas
* Usar ORM como se fosse domínio

---

# 🗂 Fonte da Verdade

Em projetos reais:

* Código é fonte primária
* Testes validam comportamento
* ADR registra decisões estruturais

Se a implementação divergir deste documento:

1. Atualizar documento
2. Ou registrar novo ADR justificando mudança

---

# 📚 Relação com outros documentos

* `architecture/clean-architecture.md`
* `architecture/ddd.md`
* `django/project-structure.md`
* `architecture/decisions.md`

---

# 📌 Nota final

Se a View ficou difícil de entender,
o problema raramente é o Django.
É a arquitetura.
