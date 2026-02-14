# Docker — Debugging (Uso Prático)

Este documento descreve **como faço debugging em ambientes Docker / Docker Compose**
de forma sistemática e previsível.

Debug não é chute.
É método.

---

# 🎯 Quando usar este guia

Use este fluxo quando:

* O container não sobe
* O serviço sobe, mas a aplicação não responde
* A aplicação sobe, mas quebra ao acessar algo
* Banco/cache não conectam
* Comportamento local ≠ comportamento no container

---

# 🧠 Princípio central

> Sempre comece pelo erro mais simples e mais próximo da infraestrutura.

Não comece:

* Refatorando código
* Alterando regra de negócio
* Reinstalando tudo sem entender

Comece por:

* Estado do container
* Logs
* Variáveis de ambiente
* Conectividade entre serviços

---

# 🔍 Passo 1 — O container está rodando?

```
docker compose ps
```

Verifique:

* Serviço está `Up`?
* Reiniciando em loop?
* Saiu com erro?

Se não estiver rodando corretamente, vá para os logs.

---

# 📜 Passo 2 — Logs são a primeira verdade

```
docker compose logs web
docker compose logs -f web
```

Procure por:

* Traceback Python
* Erro de import
* Erro de conexão (db/redis)
* Variável de ambiente ausente

Regra prática:

> Se não olhei os logs, ainda não comecei a debugar.

---

# 🧪 Passo 3 — Entrar no container

Quando logs não são suficientes:

```
docker compose exec web bash
```

(ou `sh`, dependendo da imagem)

Dentro do container, valide:

```
python --version
pip list
env | sort
ls -la
```

Perguntas úteis:

* O código está onde eu espero?
* As dependências estão instaladas?
* As variáveis de ambiente existem?

---

# 🔐 Passo 4 — Variáveis de ambiente

Erros comuns:

* `.env` não carregou
* Nome de variável errado
* Variável existe no host, mas não no container

Verifique:

```
docker compose exec web env | sort
```

Compare com:

* `.env.example`
* settings do Django

---

# 🗄️ Passo 5 — Banco de dados

Se banco não sobe:

```
docker compose logs db
```

Se app não conecta:

Verifique:

* Hostname (use `db`, não `localhost`)
* Porta correta
* Credenciais
* Healthcheck

Teste manualmente:

```
docker compose exec web python manage.py dbshell
```

---

# 🔁 Passo 6 — Cache / Redis

Teste:

```
docker compose exec redis redis-cli ping
```

Resposta esperada:

```
PONG
```

Se falhar:

* Redis não subiu
* Hostname incorreto
* URL errada

---

# 🧱 Passo 7 — Volume e código

Problemas comuns:

* Código não reflete mudanças
* Arquivos "sumiram"
* Permissão negada

Verifique:

```
ls -la /app
```

Confirme:

* Volume está montado (`.:/app`)
* Permissões corretas
* Diretório correto

---

# 🔄 Passo 8 — Rebuild consciente

Quando mudar:

* Dependências
* Dockerfile
* Imagem base

Faça rebuild:

```
docker compose down
docker compose up -d --build
```

Se suspeitar de cache quebrado:

```
docker compose build --no-cache
```

---

# 💣 Passo 9 — Reset total (último recurso)

Quando tudo parece incoerente:

```
docker compose down -v
docker compose up -d --build
```

⚠️ Atenção:

* Remove volumes
* Apaga banco de dados local
* Usar apenas em ambiente de desenvolvimento

---

# 🚫 Anti-padrões no debugging

Evitar:

* Mudar código sem olhar logs
* Apagar tudo como primeira ação
* Ignorar comportamento diferente no container
* Misturar problema de infra com problema de negócio
* Rodar comandos no host achando que afetam o container

---

# 🧠 Checklist mental rápido

Quando algo quebra, pergunte:

* O container está rodando?
* Os logs dizem algo útil?
* As env vars existem?
* O serviço externo está acessível?
* O código dentro do container é o esperado?

Responder isso resolve a maioria dos problemas.

---

# 🗂 Fonte da Verdade

* Logs do container são fonte primária de erro
* docker-compose.yml define topologia real
* Dockerfile define ambiente de execução
* Código real no container é o que importa

Se houver divergência entre documentação e comportamento:

1. Logs prevalecem
2. Código real prevalece
3. Atualizar documentação se necessário

---

# 📌 Nota final

Docker não é o problema.
Ele apenas torna problemas explícitos.

Se algo quebrou no container,
provavelmente já estava frágil antes.
