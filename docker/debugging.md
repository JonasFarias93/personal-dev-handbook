# Docker — Debugging (Uso Prático)

Este documento descreve **como eu faço debugging em ambientes Docker / Docker Compose**.

O objetivo é:
- diagnosticar problemas rapidamente
- evitar tentativas aleatórias
- criar um fluxo mental claro de investigação
- reduzir frustração quando “simplesmente não sobe”

Debug não é chute.
É método.

---

## 🎯 Quando usar este guia

Use este guia quando:

- o container não sobe
- o serviço sobe, mas a aplicação não responde
- a aplicação sobe, mas quebra ao acessar algo
- banco/cache não conectam
- comportamento local ≠ comportamento no container

---

## 🧠 Princípio central

> **Sempre comece pelo erro mais simples e mais próximo da infraestrutura.**

Não comece:
- refatorando código
- mexendo em lógica de negócio
- reinstalando tudo sem entender

Comece:
- container
- logs
- env
- dependências

---

## 🔍 Passo 1 — O container está rodando?

```bash
docker compose ps
Verifique:

o serviço está Up?

reiniciando em loop?

saiu com erro?

Se não está rodando, vá para logs.

📜 Passo 2 — Logs são a primeira verdade
docker compose logs web
docker compose logs -f web
Procure por:

traceback Python

erro de import

erro de conexão (db/redis)

erro de variável de ambiente ausente

Regra prática:

Se não olhei os logs, ainda não comecei a debugar.

🧪 Passo 3 — Entrar no container
Quando logs não são suficientes:

docker compose exec web bash
(ou sh se a imagem for mais simples)

Dentro do container, valide:

python --version
pip list
env
ls
Perguntas úteis:

o código está onde eu espero?

as dependências estão instaladas?

as variáveis de ambiente existem?

🔐 Passo 4 — Variáveis de ambiente
Erros comuns:

.env não carregou

variável com nome errado

variável existe no host, mas não no container

Verifique:

docker compose exec web env | sort
Compare com:

.env.example

settings do Django

🗄️ Passo 5 — Banco de dados
Banco não sobe
docker compose logs db
App não conecta no banco
Verifique:

hostname (db, não localhost)

porta correta

credenciais

healthcheck do serviço

Teste manualmente:

docker compose exec web python manage.py dbshell
🔁 Passo 6 — Cache / Redis
docker compose exec redis redis-cli ping
Resposta esperada:

PONG
Se falhar:

redis não subiu

hostname errado

URL incorreta

🧱 Passo 7 — Volume e código
Problemas comuns:

código não reflete mudanças

arquivos “sumiram”

permissão negada

Verifique:

ls -la /app
Confirme:

volume está montado (.:/app)

permissões corretas

você está no diretório certo

🔄 Passo 8 — Rebuild consciente
Quando mudar:

dependências

Dockerfile

base da imagem

Faça rebuild consciente:

docker compose down
docker compose up -d --build
Se suspeitar de cache quebrado:

docker compose build --no-cache
💣 Passo 9 — Reset total (último recurso)
Quando tudo parece incoerente:

docker compose down -v
docker compose up -d --build
⚠️ Atenção:

isso apaga volumes

banco de dados será perdido

Usar apenas em ambiente local.

🚫 Anti-padrões no debugging
Evitar:

sair mudando código sem olhar logs

apagar tudo como primeira ação

“funciona fora do Docker, então ignora”

misturar problema de infra com problema de negócio

rodar comandos no host achando que afetam o container

🧠 Checklist mental rápido
Quando algo quebra, pergunte:

 o container está rodando?

 os logs dizem algo útil?

 as env vars existem?

 o serviço externo está acessível?

 o código dentro do container é o esperado?

Se responder isso, 80% dos problemas se resolvem.

📌 Nota final
Docker não é o problema.
Ele só deixa problemas explícitos.

Se algo quebrou no container,
provavelmente já estava frágil fora dele.