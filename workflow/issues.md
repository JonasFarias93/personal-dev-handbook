# Issues — Modelo Pessoal de Escrita

Este documento define **como escrevo issues** em projetos.

Issue bem escrita reduz retrabalho, ambiguidade e desperdício de tempo.

Issue não é lembrete.
É contrato de execução.

---

# 🎯 Objetivo de uma Issue

Uma issue deve:

* Descrever claramente um problema ou objetivo
* Ser pequena o suficiente para executar
* Ter critério verificável de conclusão
* Estar vinculada a uma versão

Se não é executável, não é issue.

---

# 🧠 Princípio central

> Issue grande demais não é issue. É Epic.

Se a tarefa não pode ser concluída em até 1 dia de foco,
provavelmente precisa ser quebrada.

---

# 🧱 Estrutura recomendada

## 1️⃣ Título

Curto, objetivo e técnico.

Exemplo:

```
Impedir finalizacao de chamado sem itens configurados
```

---

## 2️⃣ Contexto

Responder:

* Qual é o problema?
* O que acontece hoje?
* O que deveria acontecer?

Sem contexto, a execução vira interpretação.

---

## 3️⃣ Objetivo claro

Descrever o estado desejado.

Evitar termos vagos como:

* melhorar
* ajustar
* otimizar (sem critério)

---

## 4️⃣ Critérios de Aceite

Devem ser:

* Claros
* Testáveis
* Verificáveis

Exemplo:

* Não permite finalizar chamado sem itens
* Exibe mensagem clara ao usuário
* Teste automatizado cobre o cenário

Se não é testável, está incompleto.

---

## 5️⃣ Risco

Classificar como:

* Low
* Medium
* High

Se for High:

* Avaliar necessidade de ADR

---

## 6️⃣ Versão

Definir impacto na versão:

* PATCH
* MINOR
* MAJOR

Versão deve refletir impacto real.

---

# 🔁 Relação com Branch e Commit

Uma issue normalmente gera:

* Uma branch (`feature/...`, `fix/...`)
* Um conjunto coerente de commits
* Um PR

Uma issue não deve gerar múltiplas intenções desconectadas.

---

# 🚫 Anti-padrões

Evitar:

* Issues vagas
* Múltiplos objetivos na mesma issue
* Issue sem critério de aceite
* Issue sem DoD
* Criar issue apenas para "lembrar depois"

---

# 🗂 Fonte da Verdade

* Issue descreve intenção
* Código implementa
* Testes validam
* ADR registra decisão estrutural (quando aplicável)
* Tag registra entrega

Se comportamento final divergir da issue:

1. Atualizar issue
2. Ou criar nova issue corretiva

---

# 📌 Nota final

Issue bem escrita economiza mais tempo do que qualquer ferramenta.

Clareza antes de código.
