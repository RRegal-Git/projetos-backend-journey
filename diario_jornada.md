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


