# Release — Guia Pessoal de Entrega

Este documento define **como eu faço releases** (entregas) em projetos Git.

O objetivo é garantir que a `main` represente um estado confiável,
e que entregas sejam rastreáveis por versão/tag.

---

## 🎯 Objetivo de um release

Um release serve para:

- marcar um **estado entregável**
- criar **rastreabilidade** (o que entrou, quando entrou)
- facilitar rollback (voltar para uma versão anterior)
- comunicar evolução do projeto (mesmo que só para mim)

Release não é só “merge na main”.
Release é **um marco**.

---

## 🧠 Regra fundamental

> **A `main` deve ser sempre entregável.**

A `main` recebe apenas conteúdo que eu aceito colocar em produção
ou considerar como versão estável do projeto.

---

## 🧱 Conceitos usados

### Tag
Um “apelido” que aponta para um commit específico.

Uso: marcar o commit exato de uma entrega.

---

### Versão (SemVer)
Uso **Semantic Versioning**:

- **MAJOR**: quebra compatibilidade (mudança incompatível)
- **MINOR**: nova funcionalidade compatível
- **PATCH**: correção compatível

Formato: `MAJOR.MINOR.PATCH`  
Exemplo: `1.4.2`

---

## 🧭 Quando fazer release

Eu faço release quando:

- existe um conjunto de mudanças que faz sentido “fechar”
- há valor em versionar (deploy, entrega, marco técnico)
- uma correção importante foi finalizada
- um ciclo de desenvolvimento terminou (mesmo que pequeno)

Não faço release para “qualquer merge”.

---

## 🔁 Fluxo padrão de release (com `develop`)

1. Garantir que `develop` está estável (build/test mínimos ok)
2. Promover `develop` para `main`
3. Criar tag com versão
4. (Opcional) atualizar `CHANGELOG.md` se o projeto usar
5. (Opcional) gerar release no GitHub/GitLab com notas

---

## 🔁 Fluxo simples (sem `develop`)

1. Feature/Fix branch → PR → `main`
2. Quando fizer sentido, criar tag de versão no commit mergeado

---

## 🏷️ Padrão de tags

Formato adotado:

- `vMAJOR.MINOR.PATCH`

Exemplos:

- `v0.1.0`
- `v1.0.0`
- `v1.2.3`

---

## 📝 Notas de release (release notes)

As notas devem responder:

- O que mudou?
- Para quem isso importa?
- Há alguma migração/atenção necessária?

Regra prática:
- listar mudanças por categoria (feat/fix/refactor/chore/docs)
- manter curto e útil

---

## 🧰 Checklist rápido de release

Antes de promover para `main`:

- [ ] `develop` (ou branch alvo) está estável
- [ ] testes/lint mínimos rodaram
- [ ] mudanças estão coerentes para uma entrega
- [ ] não existem commits “genéricos” ou quebrados
- [ ] dependências/configs foram revisadas (se houver)

Antes de criar tag:

- [ ] versão escolhida faz sentido (SemVer)
- [ ] tag aponta para o commit correto na `main`

---

## ❌ Anti-padrões

Evitar:

- release sem critério (“tag toda hora”)
- versionamento que não reflete impacto real
- `main` recebendo código quebrado “só pra guardar”
- tags sem padrão (ex: `release-final-agora-vai`)

---

## 📌 Observação prática

Mesmo em projetos pessoais, **taggear versões vale muito**:
- facilita comparar mudanças
- ajuda a entender evolução
- permite voltar rapidamente para um estado conhecido
