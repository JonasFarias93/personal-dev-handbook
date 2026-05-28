# Python — venv vs Conda (Decisão Consciente)

Este documento registra **como escolho ambientes Python (`venv` ou `conda`)**.
Ele responde **qual** ferramenta usar — não como usá-la.
Para o fluxo de uso com `venv`, consulte `python/uv.md`.

Ambiente é infraestrutura.
Infraestrutura é decisão.

---

# 🎯 Problema que esta decisão resolve

Sem uma decisão clara sobre ambiente, surgem:

* Conflitos de dependência
* Versões diferentes entre máquinas
* "Funciona na minha máquina"
* Setup difícil de reproduzir
* Perda de tempo configurando ambiente

Este documento existe para evitar esse caos.

---

# 🧠 Princípio central

> Ambiente deve ser simples, previsível e reproduzível.

Se exige explicação longa para rodar,
provavelmente não é a escolha ideal.

---

# 🐍 `venv` — quando utilizo

Uso **`venv`** quando:

* Projeto é backend/web (Django, FastAPI, Flask)
* Dependências são majoritariamente Python puro
* Deploy usa Docker ou ambiente Linux padrão
* Projeto será compartilhado com outros devs backend
* Quero alinhamento com produção

### Vantagens

* Nativo do Python
* Simples e previsível
* Excelente integração com Docker
* Menos abstração oculta

### Limitações

* Dependências de sistema precisam ser resolvidas fora
* Pode ser desconfortável para libs científicas pesadas

---

# 🧪 `conda` — quando utilizo

Uso **Conda** quando:

* Trabalho com ciência de dados
* Uso bibliotecas com dependências nativas pesadas
  (NumPy, SciPy, TensorFlow, etc.)
* Preciso gerenciar Python + dependências não-Python
* O ambiente não será dockerizado

### Vantagens

* Resolve dependências binárias complexas
* Excelente para Data Science
* Ambientes isolados completos

### Limitações

* Mais pesado
* Menos alinhado com produção web
* Não reflete diretamente ambiente final de deploy

---

# 🧠 Regra prática consolidada

* Backend / APIs / Web → `venv` (+ `uv` como interface)
* Data Science / ML / Pesquisa → `conda`

Evito misturar ambos no mesmo projeto.

---

# 🧱 Organização com `venv`

Estrutura típica:
project/
├── .venv/      # fora do Git
├── pyproject.toml
├── README.md
└── web/ ou src/

Regras:

* `.venv` nunca entra no Git
* Dependências declaradas no `pyproject.toml`
* Setup documentado no README
* Uso `uv` como interface oficial

---

# 🧱 Organização com Conda

Padrão:

* Ambiente com nome do projeto
* `environment.yml` versionado
* Versões explícitas quando estabilidade importa

Conda é usado quando resolve problema real,
não por preferência pessoal.

---

# 🐳 Relação com Docker

Quando uso Docker:

* Dockerfile vira a fonte de verdade do ambiente
* Ambiente local é apenas suporte
* Código deve rodar igual dentro e fora do container

Para backend web:
`venv + uv + Docker` é combinação preferencial.

---

# 🚫 Anti-padrões

Evitar:

* Usar Conda sem necessidade real
* Misturar `pip` e `conda` sem entender implicações
* Não documentar como criar ambiente
* Depender de ambiente global
* Versionar `.venv`

---

# 🧠 Checklist de decisão

Antes de escolher:

* Vai para produção web?
* Será dockerizado?
* Usa libs científicas pesadas?
* Outras pessoas vão rodar isso?

Se:

* Web + Docker → `venv`
* Ciência de dados → `conda`

---

# 🗂 Fonte da Verdade

* `pyproject.toml` define dependências (venv)
* `environment.yml` define ambiente Conda
* Dockerfile define ambiente de produção
* ADR registra decisão estrutural relevante

Se ambiente divergir do declarado:

1. Recriar ambiente
2. Atualizar arquivo de definição

---

# 📚 Relação com outros documentos

* `python/uv.md` — como usar `venv` na prática (interface oficial)
* `python/pyproject.md` — declaração de dependências
* `docker/_dockerfile.md` — ambiente de container

---

# 📌 Nota final

Ambiente não é preferência pessoal.
É decisão técnica baseada em contexto.

Escolher bem aqui economiza tempo,
energia e dor de cabeça no futuro.
