═══════════════════════════════════════════════════════════════
DIÁRIO DE JORNADA – BACKEND/DATA
═══════════════════════════════════════════════════════════════


09/01/2026 – DIA 1 | Configuração de Ambiente
─────────────────────────────────────────────────────────────
Duração: ~1h (primeira sessão longa)

Setup Inicial:
• Instalei WSL2 + Ubuntu (utilizador: regal)
• Instalei VS Code + extensão WSL
• Aprendi comandos básicos: cd ~, pwd, mkdir, ls, touch

Estrutura Criada:
• ~/projetos/teste_terminal
• biblia_comandos.md
• diario_jornada.md
• notas.txt

Aprendizagens:
• Erros comuns: cd~ (precisa espaço), caminhos absolutos vs relativos
• Sincronização terminal ↔ VS Code funcionando

Estado: ✅ WSL + VS Code + estrutura de projetos pronta


09/01/2026 – DIA 2 | Git & GitHub
─────────────────────────────────────────────────────────────
Duração: ~2h30 (GitHub levou mais tempo)

Comandos Novos:
• cat, cp, mv, rm, echo >>

Python:
• Criei e corri hello.py
• Python funcionando ✅

Git Completo:
• Workflow: init → commit → remote → push
• Primeiro repo público criado
• Resolvido problema clipboard (migrei para Windows Terminal)

Repositório:
https://github.com/RRegal-Git/projetos-backend-journey

Estado: ✅ Linux + Python + GitHub funcionais


09/01/2026 – DIA 3 | Primeira API Flask
─────────────────────────────────────────────────────────────
Duração: 50min

Projeto1: API Flask Funcional:
• Criado ambiente virtual: python3 -m venv venv
• Endpoints implementados: / e /hello
• Testado localmente com sucesso

Repositório:
https://github.com/RRegal-Git/projeto1_flask

Estado: ✅ API REST Python | Portfólio +1 projeto


10/01/2026 – DIA 4 | Limpeza e Melhorias
─────────────────────────────────────────────────────────────
Duração: ~45min

Limpeza do Repositório:
• Removi venv/ do GitHub (ambiente local não deve ser versionado)
• Comando usado: git rm -r --cached venv
• Adicionei .gitignore para evitar repetição

Melhorias na API:
• Endpoint GET /health para status checks
• Error handler 404 personalizado (retorna JSON)
• Testado com curl -i

Aprendizagens:
• Diferença entre remover do Git vs remover do disco
• Boas práticas de versionamento

Estado: ✅ Repositório limpo e API profissionalizada


11/01/2026 – DIA 5 | POST e Comunicação Bidirecional
─────────────────────────────────────────────────────────────
Duração: 30min (domingo)

Conceitos Aprendidos:
• Diferença entre GET (ler) e POST (enviar)
• Headers HTTP (Content-Type: application/json)

Implementação:
• Endpoint POST /echo criado
• Recebe JSON com nome e nivel
• Testado com curl -X POST

Erro Resolvido:
• 415 Unsupported Media Type (typo no Content-Type)

Estado: ✅ API já sabe conversar (recebe e responde)


12/01/2026 – DIA 6 | Ferramentas Profissionais
─────────────────────────────────────────────────────────────
Duração: ~40min

Postman Setup:
• Instalei Postman no Windows (ligado ao WSL)
• Workspace criado: "Jornada Backend"
• Collection criada: "Projeto 1"

Testes Realizados:
• GET /health → 200 OK ✅
• POST /echo → 200 OK ✅
• Aprendi erro 405 Method Not Allowed (GET num endpoint POST)

Estado: ✅ Ambiente de testes profissional pronto


13/01/2026 – DIA 7 | Persistência em Memória (CRUD - Parte 1)
─────────────────────────────────────────────────────────────
Duração: ~50min

Conceito Central:
• Persistência de dados em memória RAM (lista global)

Implementação:
• Lista global: tarefas = []
• GET /tarefas → Listar todas
• POST /tarefas → Criar nova (append + 201 Created)

Fluxo Testado no Postman:
1. GET inicial → []
2. POST Tarefa 1
3. POST Tarefa 2
4. GET final → [Tarefa1, Tarefa2]

Aprendizagem Crítica:
• Dados persistem enquanto servidor corre
• Dados perdem-se ao reiniciar (RAM é volátil)

Estado: ✅ CRUD parcial (Create + Read)


15/01/2026 – DIA 8 | Read by ID (CRUD - Parte 2)
─────────────────────────────────────────────────────────────
Duração: ~45min

Objetivo:
Ler UMA tarefa específica pelo seu ID

Conceitos Aprendidos:
• Path Parameters no Flask: <int:id>
• Conversão automática de tipos (string → int)

Implementação:
• Rota: GET /tarefas/<int:id>
• Lógica: Loop for para encontrar ID
• Tratamento de erro: 404 se não encontrado

Debugging:
• Erro 404 inicial resolvido
• Aprendi a verificar tipos de dados (int vs string)
• Importância de reiniciar servidor após mudanças

Estado: ✅ CRUD avançado (Create, Read, Read by ID)


15/01/2026 – DIA 9 | CRUD Completo + Requirements
─────────────────────────────────────────────────────────────
Duração: ~1h

CRUD Finalizado:
• PUT /tarefas/<id> → Atualizar tarefa existente
• DELETE /tarefas/<id> → Remover tarefa
• Aprendi list comprehension: [t for t in tarefas if t['id'] != id]

Teste de Fogo no Postman:
1. POST → Criar
2. GET → Ler todas
3. GET /<id> → Ler uma
4. PUT /<id> → Atualizar
5. DELETE /<id> → Apagar
✅ Ciclo completo validado

Gestão de Dependências:
• pip freeze > requirements.txt
• "Congelamento" de versões (Flask==3.0.3)
• Garante reprodutibilidade do ambiente

Estado: ✅ CRUD 100% funcional | Preparado para Docker


18/01/2026 – DIA 10 | Docker - Containerização
─────────────────────────────────────────────────────────────
Duração: 20min (00h30-00h50)

Objetivo:
Containerizar a aplicação Flask para ambiente portável

Validação:
• Dockerfile existente verificado:
  - Base: Python 3.12-slim
  - WORKDIR /app
  - EXPOSE 5000
  - CMD ["python", "app.py"]
• app.py configurado: host='0.0.0.0' (essencial para Docker)

Resolução de Problemas:
• Docker não reconhecido no WSL
• Solução: wsl --shutdown + restart terminal
• Integração WSL confirmada no Docker Desktop

Build e Teste:
• docker build -t projeto1-flask . → 9.2s (sucesso)
• docker run -p 5000:5000 projeto1-flask → API acessível
• Testado localhost:5000 no Windows ✅

Comandos Dominados:
• docker build -t nome-imagem .
• docker run -d -p 5000:5000 --name meu-contentor nome-imagem
• docker ps / docker ps -a
• docker logs <container_id>
• docker stop <container_id>
• docker rm <container_id>

Próximos Passos:
• Docker Compose para multi-contentores
• Multi-stage builds para otimização
• Gunicorn para production-ready

Estado: ✅ Aplicação containerizada | Ambiente reproduzível


═══════════════════════════════════════════════════════════════
PROGRESSO GERAL
═══════════════════════════════════════════════════════════════

Tempo Total Investido: ~9h30
Repositórios Criados: 2
  • projetos-backend-journey (diário + bíblia)
  • projeto1_flask (API CRUD completa)

Skills Desbloqueadas:
✅ Linux/WSL2 (navegação, gestão ficheiros)
✅ Python (virtualenv, scripts)
✅ Git & GitHub (workflow completo)
✅ Flask (API REST, CRUD, JSON)
✅ HTTP (métodos, status codes, headers)
✅ Postman (testes profissionais)
✅ Docker (containerização, imagens, contentores)

Próximas Metas:
• Docker Compose
• Base de dados (PostgreSQL/SQLite)
• Autenticação (JWT)
• Deploy (Render/Railway)


19/01/2026 – DIA 11 | Docker Compose - Orquestração
─────────────────────────────────────────────────────────────
Duração: 35min (23h20-23h55)

Objetivo:
Simplificar gestão de contentores com Docker Compose

Implementação:
• Criado .dockerignore para otimizar builds
  - Exclui: venv/, __pycache__/, .git/, .vscode/
  - Resultado: imagem mais leve e builds mais rápidos
  
• Criado docker-compose.yml:
  - Serviço 'web' com build local
  - Port mapping 5000:5000
  - Container name personalizado
  - Restart policy: unless-stopped
  - Network criada automaticamente

Comandos Dominados:
• docker compose up → Build + start tudo
• docker compose up -d → Background mode
• docker compose down → Parar e remover contentores
• docker compose logs -f → Ver logs em tempo real
• docker compose ps → Ver status dos serviços
• docker compose up --build → Rebuild após mudanças

Resolução de Problemas:
• Docker não reconhecido no WSL após reinício
• Solução: wsl --shutdown + restart terminal

Vantagem Principal:
Substituir 4+ comandos docker por apenas: docker compose up

Estado: ✅ Orquestração funcional | Preparado para multi-contentores



═══════════════════════════════════════════════════════════════
FIM DO DIÁRIO
═══════════════════════════════════════════════════════════════
