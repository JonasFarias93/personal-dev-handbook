# Arquitetura — <Nome do Projeto>

Este documento descreve a **arquitetura do projeto** e as principais decisões
que orientam sua estrutura, limites e evolução.

Ele responde:

> Como este sistema está organizado e por quê?

---

# 🗂 Metadados obrigatórios

**Última revisão:** YYYY-MM-DD
**Fonte:**

* Estrutura real do código (caminho relevante)
* Testes automatizados
* ADRs em `architecture/decisions.md`

Se houver divergência entre este documento e o código,
o código é a fonte primária.

---

# 🎯 Objetivo arquitetural

Descrever:

* Que problema o sistema resolve
* Quais qualidades são priorizadas (ex: clareza, testabilidade, escalabilidade)
* O que é conscientemente evitado

Arquitetura deve refletir intenção estratégica.

---

# 🧠 Princípios adotados

Listar princípios que guiam decisões técnicas.

Exemplos:

* Separação clara de responsabilidades
* Domínio independente de framework
* Dependências apontam para dentro
* Simplicidade antes de abstração prematura
* Testabilidade como requisito estrutural

> Decisões formais devem estar registradas em `architecture/decisions.md`.

---

# 🏗 Estilo arquitetural adotado

Descrever o estilo escolhido e por quê.

Exemplos:

* Clean Architecture
* DDD
* Arquitetura em camadas
* MVT (Django como adapter)

Explicar **como ele se manifesta na prática**, não teoria.

---

# 🧱 Camadas / Componentes

Descrever as principais camadas ou contextos.

Para cada componente:

## <Camada / Contexto>

**Responsabilidade**

* O que faz
* O que não faz

**Depende de**

* (ex: domain, application)

**Não depende de**

* (ex: web, infra)

Manter limites explícitos.

---

# 🔁 Fluxos principais

Descrever fluxos centrais do sistema.

Exemplos:

* Criação de entidade
* Execução de regra de negócio
* Entrada via API / UI
* Persistência

Preferir:

* Texto claro
* Pseudo-diagramas simples
* Sequência lógica de camadas

---

# 📦 Dependências e integrações

Listar dependências relevantes:

* Banco de dados
* Serviços externos
* Bibliotecas críticas

Explicar:

* Onde se conectam
* Em qual camada vivem
* Como são isoladas do domínio

---

# 🧪 Testabilidade

Explicar como a arquitetura facilita:

* Testes unitários
* Testes de aplicação
* Testes de integração
* Isolamento de regra de negócio

Se for difícil testar, justificar.

---

# ⚖️ Trade-offs aceitos

Nenhuma arquitetura é perfeita.

Listar conscientemente:

* O que foi simplificado
* O que foi sacrificado
* Dívida técnica assumida

Trade-offs devem ser conscientes.

---

# 🔄 Evolução esperada

Descrever:

* Pontos de extensão planejados
* Riscos conhecidos
* Áreas sensíveis a mudança
* Possíveis refatorações futuras

---

# 📚 Referências internas

* `architecture/decisions.md`
* `README.md`
* `security/django.md` — decisões de segurança relevantes
* `observability/logging.md` — estratégia de logs
* Documentos de domínio específicos
* Workflow / Roadmap (quando relevante)

---

# 📌 Notas finais

Qualquer observação relevante:

* Decisões temporárias
* Alertas para o futuro
* Armadilhas já conhecidas

---

# 🗂 Regra final

Arquitetura não documentada vira suposição.

Se uma decisão foi relevante o suficiente para gerar discussão,
ela deve estar registrada em ADR.
