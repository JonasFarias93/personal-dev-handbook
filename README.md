# Dev Notes — Referência Técnica Pessoal

Este repositório é um **arquivo pessoal de referência técnica consolidada**.

Ele registra como eu estruturo projetos, tomo decisões e organizo execução.
Não é apenas sobre ferramentas — é sobre **padrões validados na prática**.

> Não é tutorial.
> Não é documentação corporativa.
> É um sistema pessoal de engenharia.

---

# 🎯 Objetivo

* Centralizar padrões consolidados de desenvolvimento
* Registrar decisões técnicas validadas na prática
* Evitar reaprender do zero a cada projeto
* Servir como base inicial para novos projetos
* Reduzir fricção em decisões recorrentes

Este repositório deve permitir que eu retome qualquer projeto — mesmo meses depois — com clareza estrutural e consistência.

---

# 🧠 Como usar este repositório

Use como:

* 📖 Consulta rápida de padrões já definidos
* 📋 Fonte de templates reutilizáveis
* 🧭 Validador de decisões antes de implementar algo novo

### Exemplos práticos

* Antes de criar commits → `git/commits.md`
* Antes de definir branches → `git/branching.md`
* Antes de fazer release → `git/release.md`
* Antes de estruturar arquitetura → `architecture/`
* Antes de configurar Python → `python/`
* Antes de configurar CI → `workflow/ci.md`
* Antes de abrir Issues → `workflow/issues.md`

---

# 🧱 Sistema de Engenharia

Este handbook está organizado como um **sistema completo de engenharia**:

## 🏗 Arquitetura

* `architecture/clean-architecture.md`
* `architecture/ddd.md`
* `architecture/decisions.md` (ADR)

Define como estruturo sistemas e tomo decisões arquiteturais.

---

## 🐍 Python

* `python/pyproject.md`
* `python/testing.md`
* `python/uv.md`
* `python/venv-vs-conda.md`

Define ambiente, dependências, testes e padrão oficial de setup.

---

## 🌐 Django

* `django/mvt.md`
* `django/project-structure.md`
* `django/settings.md`

Define como adapto Django à arquitetura, não o contrário.

---

## 🐳 Docker

* `docker/_dockerfile.md`
* `docker/compose.md`
* `docker/debugging.md`

Define ambiente containerizado previsível e reproduzível.

---

## 🌿 Git

* `git/commits.md`
* `git/branching.md`
* `git/release.md`

Define versionamento, fluxo de branches e política de releases.

---

## ⚙️ Workflow (Governança)

* `workflow/roadmap.md`
* `workflow/issues.md`
* `workflow/DoD.md`
* `workflow/github-projects.md`
* `workflow/ci.md`

Define execução, qualidade e gestão técnica.

---

## 📦 Templates

* `templates/README-template.md`
* `templates/architecture-template.md`

Modelos reutilizáveis para iniciar novos projetos com consistência.

---

# 🗂 Estrutura do repositório

```
personal-dev-handbook/
├── architecture/
├── python/
├── django/
├── docker/
├── git/
├── workflow/
├── templates/
├── CONTRIBUTING.md
└── README.md
```

Cada arquivo deve responder uma pergunta clara.

Se um documento não orienta decisão real,
ele deve ser simplificado ou removido.

---

# ✍️ Padrão de escrita

Sempre que possível, documentos seguem:

1. Contexto
2. Regra prática
3. Exemplos
4. Anti‑padrões
5. Checklist
6. Fonte da Verdade (quando aplicável)

Decisões estruturais relevantes devem gerar ADR.

---

# 🔄 Atualização

Este repositório não é atualizado por obrigação.

Atualizar somente quando:

* Uma decisão mudou de forma consistente
* Um padrão foi validado em múltiplos projetos
* Um erro relevante precisa ser registrado

Aprendizado temporário não entra aqui.

---

# 🧭 Princípios

* Clareza > completude
* Decisão explícita > convenção implícita
* Processo > ferramenta
* Simplicidade sustentável > complexidade prematura
* Consistência entre projetos > inovação desnecessária

---

# 🚧 Status

Este repositório é vivo, mas não volátil.

Ele evolui conforme experiência real se consolida.

---

# 🤝 Contribuindo

Veja `CONTRIBUTING.md`.

---

# 📌 Nota final

Se este documento deixar de refletir minha prática real,
a primeira ação deve ser atualizá-lo.

Handbook desatualizado é pior do que nenhum handbook.
