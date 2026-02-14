# Branching — Fluxo Pessoal de Branches

Este documento define **como organizo branches em projetos Git**,
alinhado com versionamento consciente, ADR e histórico sustentável.

Branching é mecanismo de controle de risco.

---

# 🎯 Objetivo do fluxo de branches

* Evitar commits diretos em branch estável
* Isolar trabalho em progresso
* Reduzir conflitos e retrabalho
* Facilitar revisão (mesmo trabalhando sozinho)
* Garantir que a linha principal esteja sempre consistente

---

# 🧠 Regra fundamental

> Eu não trabalho direto na `main`.

`main` representa o estado mais próximo de entregável.

---

# 🌿 Branches principais

## `main`

### Função

* Estado estável
* Base para tags e releases
* Referência de produção (quando aplicável)

### Regras

* Sem commits diretos
* Só recebe merge vindo de `develop` ou branch de release
* Deve estar sempre funcional

---

## `develop`

### Função

* Branch de integração contínua
* Base para features, fixes e refactors

### Regras

* Recebe merges frequentes
* Deve estar sempre "rodando"
* Testes mínimos devem passar

> Em projetos pequenos, posso simplificar para: `feature → main via PR`.

---

# 🧩 Branches de trabalho

## `feature/<slug>`

Usada para novas funcionalidades.

Exemplos:

```
feature/chamado-finalizar
feature/importacao-notas
```

---

## `fix/<slug>`

Usada para correções de bug.

Exemplos:

```
fix/dotenv-carregamento
fix/erro-validacao-itens
```

---

## `refactor/<slug>`

Usada para refatoração sem alterar comportamento.

Exemplos:

```
refactor/servico-finalizacao
refactor/repositorio-chamado
```

---

## `chore/<slug>`

Usada para manutenção ou infraestrutura.

Exemplos:

```
chore/atualiza-deps
chore/ci-lint
```

---

# 🔁 Fluxo padrão (dia a dia)

1. Criar branch a partir da `develop`
2. Trabalhar e commitar seguindo `git/commits.md`
3. Abrir PR (mesmo para auto‑revisão)
4. Fazer merge na `develop`
5. Quando estabilizar, promover para `main`

---

# 🧪 Integração com testes e governança

Antes de merge para `develop`:

* Testes mínimos devem passar
* Lint básico deve rodar (quando aplicável)
* Mudança tem escopo claro
* Se houver decisão estrutural → ADR criada

Antes de promover para `main`:

* `develop` está estável
* Versão foi definida (SemVer)
* Release está documentada (se aplicável)

---

# 🔄 Relação com Versionamento (SemVer)

* `main` representa versão estável
* Tags devem ser criadas a partir de `main`
* `develop` pode conter trabalho ainda não versionado

Se a mudança quebra contrato público,
revisar política de versão antes de merge em `main`.

---

# ❌ Anti‑padrões

Evitar:

* Trabalhar dias sem integrar com `develop`
* Misturar feature + refactor + chore no mesmo branch
* Criar branch a partir de branch desatualizada
* Merge em `main` com build/test quebrados

---

# 🧠 Checklist rápido

Antes de merge:

* Branch está atualizada com `develop`
* Commits seguem padrão
* Testes rodaram
* Escopo está claro
* ADR criada se necessário

---

# 🗂 Fonte da Verdade

* Histórico Git é fonte da evolução
* `main` representa estado estável
* Tags representam versões oficiais
* ADR registra decisões estruturais

Se histórico divergir da documentação,
o Git prevalece.

---

# 📌 Nota final

Branching disciplinado reduz conflito,
diminui risco
e facilita evolução sustentável do projeto.
