# Dev Notes — Referência Técnica Pessoal

Este repositório é um **arquivo pessoal de referência técnica**.

Ele existe para registrar **como eu decido fazer as coisas**, não apenas *como elas funcionam*.  
É um apoio de memória para padrões, decisões, processos e boas práticas que eu quero repetir conscientemente ao longo do tempo.

> Não é um tutorial.  
> Não é documentação corporativa.  
> É um guia prático escrito para mim mesmo.

---

## 🎯 Objetivo

- Centralizar **padrões pessoais** de desenvolvimento
- Registrar **decisões técnicas** e o *porquê* delas
- Evitar reaprender do zero a cada projeto
- Servir como base para documentações de outros projetos
- Reduzir fricção em decisões recorrentes (Git, arquitetura, setup, etc.)

---

## 🧠 Como usar este repositório

Este repositório deve ser usado como:

- 📖 **Consulta rápida**
- 📋 **Fonte de templates**
- 🧭 **Validador de decisões técnicas**

### Exemplos práticos

- Antes de criar commits → consultar `git/commits.md`
- Antes de estruturar um projeto → consultar `architecture/`
- Antes de configurar ambiente Python → consultar `python/`

---

## 🗂️ Estrutura

A organização segue **áreas de conhecimento**, não projetos específicos.
```
dev-notes/
├── git/ # Versionamento, fluxo, commits
├── python/ # Ambiente, dependências, testes
├── django/ # Estrutura, MVT, boas práticas
├── docker/ # Dockerfile, compose, debug
├── architecture/ # DDD, Clean Architecture, decisões
├── templates/ # Templates reutilizáveis
└── README.md
```

Cada arquivo deve responder **uma pergunta clara**.

---

## ✍️ Padrão de escrita dos documentos

Todo documento deve seguir, sempre que possível, este formato:

1. **Contexto** — quando isso se aplica  
2. **Regra pessoal** — como eu decido fazer  
3. **Exemplo prático**  
4. **Anti-padrões** — o que evitar  
5. **Checklist** — validação rápida  

Se não for possível responder essas partes, o documento ainda não está maduro.

---

## 🔄 Atualização dos conteúdos

Este repositório **não é atualizado por obrigação**.

Atualizar somente quando:

- uma decisão mudou
- um padrão se mostrou ruim
- um novo aprendizado foi consolidado
- um erro merece ser registrado para não se repetir

Aprendizado temporário **não entra aqui**.

---

## 🧱 Princípios

- Clareza > completude
- Decisão explícita > convenção implícita
- Processo > ferramenta
- Simplicidade sustentável > complexidade prematura

---

## 🚧 Status

Este repositório é **vivo**, mas **não volátil**.  
Ele evolui lentamente, conforme experiência real se acumula.

---

## 🤝 Contribuindo

Sugestões e correções são bem-vindas via Issues.
Veja `CONTRIBUTING.md`.

---

## 📌 Nota final

Se um dia este repositório deixar de fazer sentido,  
isso significa que meus critérios mudaram — e isso também é aprendizado.
