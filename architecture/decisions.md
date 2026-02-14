# Architecture Decisions

Este documento define o **modelo oficial de ADR (Architecture Decision Record)**
que deve ser utilizado em todos os projetos.

Ele existe para:

* Tornar decisões estruturais explícitas
* Garantir rastreabilidade ao longo do tempo
* Evitar rediscussões desnecessárias
* Preservar contexto para o “eu do futuro”
* Estabelecer um padrão replicável entre projetos

---

# 🎯 Princípio Fundamental

> Decisão estrutural sem registro formal é apenas uma suposição compartilhada.

---

# 📐 Modelo Oficial de ADR

Cada projeto deve possuir seu próprio diretório de decisões (ex: `DECISIONS/`).

A numeração é **sequencial por projeto**:

ADR-001
ADR-002
ADR-003
...

IDs não devem ser reutilizados.

---

## 🧱 Estrutura obrigatória de cada ADR

**ID**
ADR-XXX

**Data**
YYYY-MM-DD

**Status**
Proposto | Aceito | Deprecado

**Decisão**
Descrição clara e objetiva do que foi decidido.

**Contexto**
Problema, risco ou ambiguidade existente no momento da decisão.

**Consequências**
Impactos esperados:

* trade-offs
* ganhos
* perdas
* limitações futuras

---

# 🗂 Organização recomendada

Em projetos pequenos, ADRs podem ficar em lista simples.

Em projetos médios/grandes, recomenda-se:

* Índice por domínio
* Separação por contexto (Architecture, Domain, UI, Testing, etc.)
* Tabela com ID, título, data e status

O modelo usado no Expansao360 é considerado referência de maturidade.

---

# 🔄 Política de Evolução

* ADRs **não devem ser removidos**.
* Mudanças estruturais exigem novo ADR.
* Novo ADR deve referenciar o anterior.
* Status deve refletir estado atual.

Deprecar não apaga o passado — apenas registra evolução.

---

# 📚 Quando registrar uma decisão

Registrar quando a decisão:

* Impacta arquitetura ou estrutura do projeto
* Afeta múltiplas camadas ou módulos
* Define padrão recorrente
* Impõe restrições futuras
* Resolve ambiguidade estrutural relevante
* Contraria prática comum deliberadamente

Decisões triviais ou temporárias **não entram aqui**.

---

# 🗂 Metadados obrigatórios em documentação de projeto

Toda documentação estrutural futura (ADR, contratos técnicos, decisões de domínio, etc.)
deve conter no topo:

**Última revisão:** YYYY-MM-DD
**Fonte:**

* Código real (caminhos relevantes)
* Testes automatizados relacionados
* ADRs vinculadas

---

# 🧭 Regra de Fonte da Verdade (Source of Truth)

* O código é a fonte primária.
* Testes automatizados validam comportamento.
* ADR registra intenção estrutural.

Se documentação divergir do código:

1. O código prevalece.
2. A documentação deve ser atualizada.
3. Se a divergência for estrutural, criar novo ADR.

---

# 📌 Nota Final

Uma decisão importante o suficiente para gerar discussão
é importante o suficiente para ser registrada.

Se a documentação não aponta sua fonte de verdade,
elas não é confiável.
