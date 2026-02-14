# GitHub Projects — Modelo Pessoal de Gestão

Este documento define **como utilizo GitHub Projects** para organizar trabalho,
alinhado com governança técnica, versionamento consciente e execução previsível.

GitHub Projects não é só quadro de tarefas.
É sistema de controle de evolução do produto.

---

# 🎯 Objetivo do uso de Projects

Uso GitHub Projects para:

* Quebrar trabalho em unidades pequenas e executáveis
* Tornar risco explícito
* Controlar versão de entrega
* Evitar tarefas ambíguas
* Manter previsibilidade de evolução

---

# 🧠 Princípio central

> Toda issue deve ser pequena, clara e executável.

Se uma issue parece vaga ou grande demais,
ela ainda não está pronta para entrar em execução.

---

# 🗂 Estrutura do Board

Campos que utilizo:

* **Title**
* **Status**
* **Type**
* **Area**
* **Risk**
* **DoD (Definition of Done)**
* **Order**
* **Versão**

---

# 🧩 Definição dos Campos

## Status

Fluxo típico:

* Backlog
* Ready
* In Progress
* Review
* Done

Status deve refletir estado real.

---

## Type

Tipos utilizados:

* Epic
* Feature
* Task
* Bug
* TechDebt

Regras:

* Epic é grande e gera Features
* Feature gera Tasks
* Bug é correção específica
* TechDebt é melhoria estrutural

---

## Area

Define onde a mudança impacta:

* Backend
* Frontend
* Infra
* Database
* Tests
* Docs
* Security
* Data

Area ajuda a entender impacto técnico.

---

## Risk

Classificação:

* Low
* Medium
* High

Regra prática:

* Low → impacto localizado
* Medium → pode afetar fluxo existente
* High → altera arquitetura ou contrato

Se risco for High, avaliar necessidade de ADR.

---

## DoD (Definition of Done)

Checklist objetivo e verificável.

Exemplos:

* Testes escritos e passando
* Lint ok
* Documentação atualizada
* Sem TODO pendente

Sem DoD claro, a tarefa não está pronta.

---

## Order

Define prioridade relativa.

Menor número → maior prioridade.

Serve para evitar decisão emocional do "o que fazer agora".

---

## Versão

Toda issue relevante deve estar vinculada a uma versão.

Regras:

* PATCH → correção
* MINOR → nova funcionalidade
* MAJOR → quebra de contrato

Versão deve refletir impacto real da mudança.

---

# 🔁 Fluxo de trabalho integrado

1. Criar issue pequena e clara
2. Definir Type, Area, Risk, DoD e Versão
3. Mover para Ready
4. Criar branch correspondente
5. Desenvolver e commitar seguindo padrão
6. Abrir PR
7. Merge em develop
8. Promover para main via release

Projects conecta planejamento → código → versão.

---

# 🧠 Relação com ADR

Se a issue:

* Altera arquitetura
* Muda boundary
* Introduz padrão novo
* Impacta múltiplos contextos

Então deve gerar ADR.

Projects não substitui ADR.
Eles se complementam.

---

# 🚫 Anti-padrões

Evitar:

* Issues genéricas ("melhorar sistema")
* Issue grande demais
* Sem DoD
* Sem versão definida
* Misturar múltiplos objetivos em uma única issue

---

# 🗂 Fonte da Verdade

* Issue descreve intenção
* Código implementa comportamento
* Testes validam resultado
* ADR registra decisão estrutural
* Tag registra entrega

Se houver divergência:

1. Código prevalece
2. Atualizar issue ou documentação
3. Registrar ADR se necessário

---

# 📌 Nota final

GitHub Projects organiza execução.
Git organiza história.
ADR organiza decisões.

Juntos, formam governança completa do projeto.
