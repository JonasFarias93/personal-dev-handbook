# Roadmap — Modelo Pessoal de Planejamento

Este documento define **como estruturo um roadmap** para projetos.

Roadmap não é lista de tarefas.
É visão estratégica organizada no tempo.

---

# 🎯 Objetivo do Roadmap

O roadmap serve para:

* Definir direção
* Organizar prioridades
* Comunicar evolução esperada
* Evitar desenvolvimento reativo
* Conectar visão → execução

Roadmap responde:

> O que vem depois e por quê?

---

# 🧠 Princípio central

> Roadmap organiza ÉPICOS, não tasks.

Tasks vivem no GitHub Projects.
Roadmap organiza grandes blocos estratégicos.

---

# 🧱 Estrutura recomendada

## 1️⃣ Horizonte temporal

Organizar por:

* Versão (ex: v1.0, v1.1, v2.0)
  OU
* Trimestre (Q1, Q2, etc.)
  OU
* Marco estratégico (MVP, Beta, Produção)

Escolher apenas um modelo por projeto.

---

## 2️⃣ Blocos de entrega (Epics)

Cada item do roadmap deve representar:

* Um Epic
* Um grande objetivo funcional
* Um marco arquitetural

Exemplo:

```
v1.0.0 — Marco Produção

- Chamados operacionais completos
- Execução com sessão exclusiva
- IAM mínimo funcional
- Auditoria de eventos críticos
- Postgres como banco padrão
```

---

## 3️⃣ Critério de entrada no Roadmap

Um item entra no roadmap quando:

* Tem impacto estratégico
* Exige múltiplas issues
* Representa evolução significativa

Se é pequeno, fica apenas no board.

---

# 🔁 Relação com GitHub Projects

Roadmap define direção.

GitHub Projects executa.

Fluxo:

Roadmap → Epic → Feature → Task → PR → Release

Roadmap não substitui issue.
Ele antecede issue.

---

# 📦 Versão e Roadmap

Roadmap deve estar alinhado com SemVer.

* v0.x → experimentação / consolidação
* v1.0.0 → marco estável
* v2.0.0 → evolução estrutural

Se uma entrega altera arquitetura relevante,
considerar ADR associada.

---

# 🧪 Roadmap técnico vs funcional

Pode conter:

Funcional:

* Nova capacidade do sistema
* Nova área de negócio

Técnico:

* Migração de banco
* Reorganização arquitetural
* Introdução de CI
* Padronização de testes

Ambos são válidos.

---

# 🚫 Anti-padrões

Evitar:

* Roadmap com tasks pequenas
* Roadmap reativo (apenas bugs)
* Roadmap sem horizonte temporal
* Roadmap que não conversa com versão
* Roadmap que nunca é revisado

---

# 🔄 Revisão do Roadmap

Revisar quando:

* Uma versão é concluída
* Estratégia muda
* Arquitetura evolui
* Escopo cresce além do esperado

Roadmap não é fixo.
Mas também não deve mudar semanalmente.

---

# 🗂 Fonte da Verdade

* Roadmap define intenção estratégica
* GitHub Projects executa
* Git registra evolução
* Tags marcam entregas
* ADR registra decisões estruturais

Se roadmap divergir da realidade do projeto:

1. Atualizar roadmap
2. Ou registrar decisão explicando mudança

---

# 📌 Nota final

Sem roadmap, o projeto reage.

Com roadmap, o projeto evolui
