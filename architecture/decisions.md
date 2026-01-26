# Architecture Decisions

Este documento registra **decisões técnicas e arquiteturais relevantes**,  
com o objetivo de **evitar ambiguidades**, **manter rastreabilidade** e  
**facilitar onboarding** (inclusive do “eu do futuro”).

Ele documenta **o porquê das escolhas**, não apenas o resultado final.

---

## 🎯 Objetivo

- Tornar decisões arquiteturais explícitas
- Preservar contexto ao longo do tempo
- Evitar discussões recorrentes sobre decisões já tomadas
- Facilitar revisões conscientes de decisões passadas
- Criar histórico de aprendizado técnico

---

## 🧭 Quando registrar uma decisão

Uma decisão deve ser registrada aqui quando:

- impacta a arquitetura ou estrutura do projeto
- afeta múltiplas camadas ou módulos
- define um padrão recorrente
- impõe restrições futuras
- resolve ambiguidades relevantes
- contraria práticas comuns de forma deliberada

Decisões triviais **não entram aqui**.

---

## 🧱 Formato padrão das decisões

Cada decisão registrada neste documento deve seguir o formato abaixo:

**Data**  
YYYY-MM-DD

**Decisão**  
Descrição clara e objetiva do que foi decidido.

**Contexto**  
Motivação da decisão.  
Problema, dúvida ou risco que existia no momento.

**Consequências**  
Impactos esperados da decisão:
- trade-offs
- ganhos
- perdas
- limitações futuras

---

## 📚 Registro de decisões

---

### 2026-01-20 — Documentar decisões arquiteturais explicitamente

**Decisão**  
Todas as decisões arquiteturais relevantes devem ser registradas neste documento,
seguindo o formato padrão definido acima.

**Contexto**  
Decisões arquiteturais tendem a se perder com o tempo ou virar conhecimento implícito.
Isso gera retrabalho, inconsistência e discussões repetidas sobre temas já resolvidos.

**Consequências**  
- Maior clareza sobre o estado atual da arquitetura
- Menor dependência de memória individual
- Facilidade para revisão de decisões passadas
- Custo adicional de documentação (aceito conscientemente)

---

### 2026-01-20 — Priorizar decisões explícitas em vez de convenções implícitas

**Decisão**  
Convenções arquiteturais devem ser tratadas como decisões explícitas,
e não como suposições compartilhadas.

**Contexto**  
Convenções implícitas funcionam apenas enquanto o contexto está fresco.
Com o tempo, passam a ser interpretadas de formas diferentes ou esquecidas.

**Consequências**  
- Redução de ambiguidades
- Menor dependência de contexto oral
- Maior previsibilidade arquitetural
- Esforço inicial maior de alinhamento

---

## 🔄 Revisão de decisões

Decisões **podem e devem mudar** quando o contexto muda.

Quando uma decisão deixar de fazer sentido:
- **não remover o registro**
- adicionar uma nova decisão explicando a mudança
- referenciar a decisão anterior

Isso preserva histórico e aprendizado.

---

## 📌 Nota final

Uma decisão não documentada é apenas uma suposição compartilhada.
