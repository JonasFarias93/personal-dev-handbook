# Release — Guia Pessoal de Entrega

Este documento define **como faço releases em projetos Git**,
alinhado com SemVer, governança de branches e rastreabilidade histórica.

Release não é apenas merge na `main`.
É um marco versionado e consciente.

---

# 🎯 Objetivo de um release

Um release serve para:

* Marcar um estado entregável
* Criar rastreabilidade (o que entrou e quando entrou)
* Facilitar rollback
* Comunicar evolução do projeto
* Consolidar um ciclo de trabalho

Release é um ponto de estabilidade.

---

# 🧠 Regra fundamental

> A `main` deve ser sempre entregável.

A `main` recebe apenas código que eu aceito considerar estável.

---

# 🧱 Conceitos utilizados

## Tag

Uma tag aponta para um commit específico.

Uso:

* Marcar o commit exato da entrega
* Facilitar comparação entre versões

---

## Versionamento (SemVer)

Uso **Semantic Versioning**:

* **MAJOR** → quebra compatibilidade
* **MINOR** → nova funcionalidade compatível
* **PATCH** → correção compatível

Formato:

```
MAJOR.MINOR.PATCH
```

Exemplos:

```
1.0.0
1.4.2
2.0.0
```

---

# 🔄 Relação entre commits e versão

* `feat` normalmente impacta MINOR
* `fix` impacta PATCH
* Mudança que quebra contrato pode exigir MAJOR

Se houver dúvida estrutural sobre impacto,
registrar ADR antes de definir versão.

---

# 🧭 Quando fazer release

Faço release quando:

* Existe um conjunto coerente de mudanças
* Há valor em versionar (deploy, entrega, marco técnico)
* Uma correção importante foi finalizada
* Um ciclo de desenvolvimento foi fechado

Não faço release para qualquer merge trivial.

---

# 🔁 Fluxo padrão com `develop`

1. Garantir que `develop` está estável
2. Promover `develop` para `main`
3. Criar tag com versão
4. (Opcional) Atualizar `CHANGELOG.md`
5. (Opcional) Publicar release com notas

---

# 🔁 Fluxo simplificado (sem `develop`)

1. Feature/Fix → PR → `main`
2. Quando fizer sentido, criar tag no commit da `main`

---

# 🏷️ Padrão de tags

Formato adotado:

```
vMAJOR.MINOR.PATCH
```

Exemplos:

```
v0.1.0
v1.0.0
v1.2.3
```

Tags devem sempre apontar para commit da `main`.

---

# 📝 Notas de release (Release Notes)

Notas devem responder:

* O que mudou?
* Para quem isso importa?
* Há impacto ou migração necessária?

Organizar por categoria:

* feat
* fix
* refactor
* chore
* docs

Manter conciso e útil.

---

# 🧰 Checklist rápido de release

Antes de promover para `main`:

* [ ] `develop` está estável
* [ ] Testes/lint rodaram
* [ ] Mudanças são coerentes para uma entrega
* [ ] Não há commits genéricos
* [ ] Dependências e configurações foram revisadas

Antes de criar tag:

* [ ] Versão faz sentido (SemVer)
* [ ] Tag aponta para commit correto
* [ ] Histórico está limpo

---

# 🚫 Anti-padrões

Evitar:

* Tag a cada pequeno commit
* Versionamento que não reflete impacto real
* `main` com código quebrado
* Tags sem padrão claro

---

# 🗂 Fonte da Verdade

* `main` representa estado estável
* Tags representam versões oficiais
* Histórico Git é fonte da evolução
* ADR registra decisões estruturais relevantes

Se houver divergência entre documentação e histórico,
Git prevalece.

---

# 📌 Nota final

Versionar conscientemente ajuda a entender a evolução real do sistema.

Release não é burocracia.
É clareza histórica.
