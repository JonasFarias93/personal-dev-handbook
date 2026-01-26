# Branching — Fluxo Pessoal de Branches

Este documento define **como eu organizo branches** em projetos Git.

O objetivo é manter:
- trabalho isolado (sem quebrar a linha principal)
- histórico limpo
- merge previsível
- entregas controladas

---

## 🎯 Objetivo do fluxo de branches

- Evitar commits diretos em branch “estável”
- Reduzir conflitos e retrabalho
- Facilitar revisão (mesmo que eu esteja sozinho)
- Garantir que a branch principal esteja sempre em estado consistente

---

## 🧠 Regra fundamental

> **Eu não trabalho direto na `main`.**

A `main` representa o estado mais próximo de “entregável”.

---

## 🌿 Branches principais

### `main`
**Função**
- Estado entregável / referência estável
- Onde vivem tags e releases (quando aplicável)

**Regras**
- Sem commits diretos
- Só recebe merge vindo de branch de integração (ex: `develop`) ou release

---

### `develop` (integração)
**Função**
- Integração do trabalho do dia a dia
- Base para features e correções

**Regras**
- Pode receber merges frequentes
- Deve estar sempre “rodando” (build/test mínimos passando)

> Se o projeto for pequeno ou muito simples, `develop` pode não existir.
> Nesse caso, o fluxo vira “feature → main via PR”.

---

## 🧩 Branches de trabalho

### `feature/<slug>`
Usada para desenvolvimento de novas funcionalidades.

**Quando usar**
- toda alteração que adiciona comportamento novo

**Exemplos**
- `feature/chamado-finalizar`
- `feature/importacao-notas`

---

### `fix/<slug>`
Usada para correção de bugs.

**Quando usar**
- correções em comportamento existente

**Exemplos**
- `fix/dotenv-carregamento`
- `fix/erro-validacao-itens`

---

### `refactor/<slug>`
Usada para refatoração (sem alterar comportamento).

**Quando usar**
- reestruturação interna, extração de métodos, reorganização

**Exemplos**
- `refactor/servico-finalizacao`
- `refactor/repositorio-chamado`

---

### `chore/<slug>`
Usada para mudanças de manutenção/infra.

**Quando usar**
- dependências, tooling, scripts, CI, Docker, formatação geral

**Exemplos**
- `chore/atualiza-deps`
- `chore/ci-lint`

---

## 🔁 Fluxo padrão (dia a dia)

1. Criar branch a partir da `develop`
2. Trabalhar e commitar seguindo `git/commits.md`
3. Abrir PR (mesmo que local/auto-revisão)
4. Fazer merge na `develop`
5. Quando estabilizar, promover para `main`

---

## ✅ Regras de merge

- Preferir merge via PR (mesmo sozinho) para criar “ponto de revisão”
- Evitar commits gigantes: dividir em passos lógicos
- Resolver conflitos na branch de trabalho, antes de integrar
- Manter `develop` saudável (build/test passando)

---

## ❌ Anti-padrões

Evitar:

- trabalhar dias direto em uma branch sem integrar
- misturar feature + refactor + chore no mesmo branch
- abrir branch a partir de branch antiga (desatualizada)
- merge na `main` com código quebrado ou sem rodar o mínimo

---

## 🧪 Checklist rápido

Antes de merge para `develop`:

- [ ] branch está atualizada com a `develop`
- [ ] commits seguem o padrão (`git/commits.md`)
- [ ] testes/lint mínimos rodaram
- [ ] mudança tem escopo claro (feature/fix/refactor/chore)

Antes de promover para `main`:

- [ ] `develop` está estável
- [ ] existe um motivo claro para “entregar agora”
- [ ] versão/release está definida (se aplicável)

