# Commit Guide (Conventional Commits)

Este projeto usa um padrão de commits para manter o histórico legível,
consistente e rastreável.

Cada commit deve representar **uma única intenção clara**.

---

## ✅ Formato

<tipo>(escopo): verbo + complemento


Exemplos:

feat(chamado): adiciona regra de finalização
fix(config): corrige carregamento do dotenv
docs(architecture): documenta separação web/domain
chore(docker): adiciona postgres ao compose


---

## 🧩 Tipos permitidos

- `feat` — nova funcionalidade
- `fix` — correção de bug
- `refactor` — refatoração sem mudar comportamento
- `docs` — documentação
- `test` — testes
- `chore` — infra, setup, deps, tooling
- `style` — formatação (sem impacto lógico)

---

## 🧠 Vocabulário padrão (verbo no imperativo)

Usar **sempre verbo no imperativo**, em português, iniciando a mensagem.

### Verbos recomendados (por tipo)

#### `feat`
- adiciona
- implementa
- permite
- cria
- expõe

Exemplo:
feat(domain): adiciona validação de finalização


---

#### `fix`
- corrige
- impede
- resolve
- ajusta

Exemplo:
fix(chamado): impede finalização sem itens


---

#### `refactor`
- extrai
- reorganiza
- simplifica
- renomeia
- remove duplicação de

Exemplo:
refactor(execucao): extrai serviço de finalização


---

#### `docs`
- documenta
- atualiza
- adiciona
- esclarece

Exemplo:
docs(git): documenta padrão de commits


---

#### `test`
- adiciona
- cobre
- ajusta
- melhora

Exemplo:
test(chamado): adiciona cobertura para validação


---

#### `chore`
- atualiza
- adiciona
- remove
- configura

Exemplo:
chore(deps): atualiza dependências do projeto


---

#### `style`
- ajusta
- formata
- organiza

Exemplo:
style: formata arquivos com black


---

## 🎯 Escopo (como escolher)

O escopo indica **onde a mudança aconteceu**.

Sugestões de escopo:

- camada: `web`, `domain`, `infra`, `config`
- módulo/app: `chamado`, `execucao`, `cadastro`
- tooling/infra: `docker`, `deps`, `ci`

Regras práticas:
- use escopos curtos e consistentes
- evite escopos vagos (`misc`, `stuff`, `updates`)

---

## 🧠 Regras rápidas de validação

Antes de commitar, pergunte:

- Esse commit faz **uma coisa só**?
- O verbo descreve claramente a ação?
- Eu entenderia essa mensagem sem abrir o diff?
- Isso faria sentido daqui a 6 meses?

Se não → divida ou reescreva.

---

## ❌ Anti-padrões (evitar)

Mensagens genéricas ou vagas:

update
ajustes
fix
testes
wip


Esses commits não comunicam intenção.

---

## 🧪 Commits e testes

- `feat` → idealmente acompanhado de teste
- `fix` → idealmente com teste que reproduz o bug
- `refactor` → testes existentes devem continuar passando