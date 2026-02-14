# Definition of Done (DoD) — Modelo Pessoal

Este documento define **o que significa uma tarefa estar realmente pronta**.

Done não é "funciona na minha máquina".
Done é critério objetivo atendido.

---

# 🎯 Objetivo do DoD

O DoD serve para:

* Evitar entregas incompletas
* Reduzir retrabalho
* Garantir qualidade mínima
* Tornar conclusão verificável

Sem DoD claro, "feito" vira subjetivo.

---

# 🧠 Princípio central

> Se não é verificável, não está pronto.

---

# ✅ DoD padrão mínimo

Uma issue só pode ir para **Done** quando:

* [ ] Código implementado conforme objetivo
* [ ] Testes escritos (quando aplicável)
* [ ] Testes passando
* [ ] Sem erro de lint crítico
* [ ] Sem TODO pendente
* [ ] Critérios de aceite atendidos
* [ ] Commit segue padrão

---

# 🧪 DoD técnico (quando aplicável)

Para mudanças de comportamento:

* [ ] Teste automatizado cobre o cenário principal
* [ ] Cenários negativos considerados
* [ ] Regressões protegidas

Para mudanças estruturais:

* [ ] ADR criada (se necessário)
* [ ] Documentação atualizada

Para mudanças de infra:

* [ ] Ambiente sobe corretamente
* [ ] Sem segredos no repositório

---

# 🔁 Relação com Versionamento

Antes de marcar como Done:

* Versão impactada está definida
* Impacto (PATCH/MINOR/MAJOR) faz sentido

---

# 🚫 Anti-padrões

Evitar marcar como Done quando:

* "Depois eu escrevo teste"
* "Funciona mas não revisei"
* "Tem um TODO mas resolvo depois"
* "Lint quebrou mas ignora"

---

# 🗂 Fonte da Verdade

* Código implementado
* Testes passando
* Critérios de aceite cumpridos
* Versão definida

Se algo quebrar após Done:

* Criar nova issue
* Classificar como Bug
* Avaliar falha no DoD

---

# 📌 Nota final

DoD protege o projeto do entusiasmo.

Sem critério objetivo,
"pronto" é apenas sensação.
