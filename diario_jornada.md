# Diário de Jornada – Backend/Data

## 2026-01-09 – Dia 1 (primeira sessão longa)
- Instalei WSL2 + Ubuntu (utilizador `regal`).
- Aprendi `cd ~`, `pwd`, `mkdir`, `ls`, `touch`.
- Criei estrutura: `~/projetos/teste_terminal`.
- Instalei VS Code + extensão WSL.
- Criei `notas.txt` e confirmei sincronização terminal ↔ VS Code.
- Criei `biblia_comandos.md` e `diario_jornada.md`.
- Erros comuns: `cd~` (precisa espaço), caminhos absolutos vs relativos.

**Tempo total hoje:** ~1h (primeiro dia mais longo, amanhã volta aos 30-45min)
**Ambiente pronto:** ✅ WSL + VS Code + estrutura de projetos

## 2026-01-09 – Dia 2 (12h-14h)
- Comandos novos: cat, cp, mv, rm, echo >>.
- Criei/corro `hello.py` ✅ Python funcionando.
- Git completo: init → commit → remote → push.
- **PRINCIPAIS VITÓRIAS:** 
  - Primeiro repo GitHub público: https://github.com/RRegal-Git/projetos-backend-journey
  - Resolvido problema clipboard (PowerShell + WSL). --> Passei para o Windowns Terminal (download na store)
  - Bíblia + Diário profissionais.
**Tempo:** ~2h30 (GitHub levou mais tempo).
**Estado:** Linux + Python + GitHub ✅

## 2026-01-09 – Dia 3 (16h-16h50)
- **Projeto1**: API Flask funcional (endpoints `/` e `/hello`).
- Virtualenv criado (`python3 -m venv venv`).
- GitHub: https://github.com/RRegal-Git/projeto1_flask
- **Tempo**: 50min
**Estado**: API REST Python ✅ Portfólio +1 projeto

## 2026-01-10 – Dia 4 (limpeza repo + melhorias API)
- No projeto `projeto1_flask`, removi a pasta `venv/` do GitHub (era lixo de ambiente local) e adicionei `.gitignore` para impedir que volte a ser versionada.
- Usei `git rm -r --cached venv` para o Git “esquecer” a pasta no repositório sem apagar a pasta no meu computador. 
- Adicionei endpoint `GET /health` para verificação rápida do estado da API (retorna JSON com status). 
- Configurei `@app.errorhandler(404)` para devolver erros 404 em JSON (mais consistente para APIs).
- Testei com `curl -i` e confirmei: `/health` devolve 200 OK e uma rota inventada devolve 404 em JSON. 
- Fiz commit(s) e push para garantir que o GitHub fica com a versão “limpa” do projeto. 

## 2026-01-11 – Dia 5 (30 min - Domingo)
- Aprendi a diferença entre **GET** (ler) e **POST** (enviar).
- Criei endpoint `/echo` no Flask para receber e processar JSON.
- Testei com `curl -X POST` enviando dados reais (`nome`, `nivel`).
- **Erro resolvido:** 415 Unsupported Media Type (tinha typo no `Content-Type`).
- **Estado:** API já sabe conversar (recebe e responde)! ✅

## 2026-01-12 – Dia 6 (Ferramentas Profissionais)
- Instalei Postman no Windows (ligado ao WSL).
- Criei Workspace "Jornada Backend" e Collection "Projeto 1".
- Testei endpoint GET /health (Sucesso 200 OK).
- Testei endpoint POST /echo enviando JSON (body).
- Aprendi na prática o erro 405 (Method Not Allowed) ao tentar fazer GET num endpoint POST.
- **Estado:** Tenho um ambiente de testes profissional pronto para APIs mais complexas! 🚀

## 2026-01-13 – Dia 7 (Memória RAM e CRUD Básico)
- **Conceito Chave:** Persistência de Dados em Memória.
- Criei uma lista global `tarefas = []` no `app.py` para servir de base de dados temporária.
- Implementei **GET /tarefas**: Devolve a lista completa de tarefas (JSON).
- Implementei **POST /tarefas**: Recebe um JSON, adiciona à lista `tarefas` (append) e devolve 201 Created.
- Testei o fluxo completo no Postman:
  1. GET inicial (lista vazia `[]`).
  2. POST (adicionar Tarefa 1).
  3. POST (adicionar Tarefa 2).
  4. GET final (lista com 2 itens).
- **Aprendizagem:** Entendi que os dados persistem enquanto o servidor corre, mas perdem-se ao reiniciar (RAM é volátil).
- **Estado:** API já guarda dados! (Create + Read feitos). ✅

## 2026-01-15 – Dia 8 (CRUD: Read by ID)
- **Objetivo:** Criar endpoint para ler apenas UMA tarefa específica, usando o seu ID.
- Aprendi o conceito de **Path Parameters** no Flask: `<int:id>`.
- Implementei a rota `GET /tarefas/<int:id>`.
- Lógica criada: Percorrer a lista `tarefas` (loop for), encontrar o ID correspondente e devolver esse objeto.
- Tratamento de erro: Se o loop terminar sem encontrar o ID, retorna 404 Not Found.
- **Depuração:** Enfrentei um erro 404 inicial, mas resolvi verificando os tipos de dados (int vs string) e reiniciando o servidor corretamente.
- **Estado:** CRUD quase completo (Falta Update e Delete). ✅

## 2026-01-15 – Dia 9 (CRUD Completo e Preparação Docker)
- **Implementação Final do CRUD:**
  - Adicionei endpoint `PUT /tarefas/<id>` para atualizar tarefas existentes.
  - Adicionei endpoint `DELETE /tarefas/<id>` para remover tarefas.
  - Aprendi a filtrar listas em Python (`[t for t in tarefas if ...]`) para remover itens de forma segura.
- **Teste de Fogo:** Validei o ciclo de vida completo no Postman (Criar -> Ler -> Atualizar -> Apagar).
- **Gestão de Dependências:**
  - Usei `pip freeze > requirements.txt` para gerar a lista de bibliotecas instaladas.
  - Entendi que isto "congela" as versões (ex: `Flask==3.0.3`) para garantir que o projeto funciona em qualquer lugar.
- **Próximos Passos:** Dockerizar a API! 🐳

