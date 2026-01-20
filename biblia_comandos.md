# Bíblia de Comandos Linux & Backend

## ⚡ Essenciais
- `Tab` – autocomplete (completa nomes de ficheiros/comandos).
- `↑↓` – histórico de comandos usados anteriormente.
- `clear` – limpar o ecrã do terminal.
- `Ctrl+C` – parar servidor ou script que está a correr.
- `q` – sair de git diff, git log, man pages.

## 📂 Navegação
- `cd <pasta>` – mudar de diretório.
- `cd ~` – ir para o diretório home (raiz do utilizador).
- `pwd` – mostrar o caminho da pasta atual.
- `ls` – listar ficheiros da pasta atual.
- `ls -la` – listar tudo incluindo ocultos com permissões.
- `wsl` – abrir Ubuntu a partir do PowerShell Windows.

## 📄 Gestão de Ficheiros
- `mkdir <nome>` – criar diretório (pasta).
- `touch <nome>` – criar ficheiro vazio.
- `code .` – abrir VS Code na pasta atual.
- `nano ficheiro` – editor de texto simples (Ctrl+O para guardar, Ctrl+X para sair).
- `cat ficheiro` – ler conteúdo no terminal.
- `head -n 5 ficheiro` – ver primeiras 5 linhas.
- `tail -n 10 ficheiro` – ver últimas 10 linhas.
- `grep "palavra" ficheiro` – procurar texto num ficheiro.
- `grep -n "texto" ficheiro` – procurar com números de linha.
- `echo "texto" >> ficheiro` – adicionar texto ao final de um ficheiro.
- `cp origem destino` – copiar ficheiro.
- `mv origem destino` – mover ou renomear ficheiro.
- `rm ficheiro` – apagar ficheiro (cuidado: não vai para a reciclagem!).
- `rm -rf pasta/` – apagar pasta e conteúdo (use com extremo cuidado!).

## 🐍 Python & Ambiente
- `python3 ficheiro.py` – correr script Python.
- `python3 -m venv venv` – criar ambiente virtual.
- `source venv/bin/activate` – ativar ambiente (essencial!).
- `deactivate` – sair do ambiente.

## 📦 Pacotes (Pip)
- `pip install nome_pacote` – instalar biblioteca (ex: Flask).
- `pip install -r requirements.txt` – instalar dependências a partir de um ficheiro.
- `pip freeze > requirements.txt` – gerar lista de dependências instaladas ("congelar" versões).
- `pip list` – listar pacotes instalados.
- `pip uninstall nome_pacote` – desinstalar pacote.

## 🐙 Git & GitHub
- `git init` – iniciar repositório novo.
- `git status` – ver o que mudou.
- `git diff` – ver diferenças em detalhe (sair com 'q').
- `git add .` – preparar tudo para guardar.
- `git add ficheiro.py` – preparar ficheiro específico.
- `git commit -m "msg"` – gravar snapshot (histórico).
- `git push` – enviar alterações para o GitHub.
- `git push origin main` – push para branch main.
- `git pull` – buscar atualizações do remoto.
- `git log --oneline` – ver histórico de commits resumido.
- `git reset --soft HEAD~1` – desfazer último commit (mantém alterações).
- `git checkout -b nome-branch` – criar nova branch.
- `git checkout main` – mudar para branch main.
- `.gitignore` – ficheiro que lista o que o Git deve ignorar (ex: `venv/`).
- `git rm -r --cached pasta` – parar de versionar uma pasta sem a apagar do PC.
- `git config --global credential.helper store` – guardar password/token para sempre.

## 🌐 API & HTTP (Conceitos)
- `GET` – Ler dados (Safe).
- `POST` – Criar dados novos.
- `PUT` – Atualizar dados existentes (substitui tudo).
- `DELETE` – Apagar dados.
- **Códigos Comuns:**
  - `200 OK` (Sucesso).
  - `201 Created` (Criado com sucesso).
  - `404 Not Found` (Não encontrado).
  - `415 Unsupported Media Type` (Falta header Content-Type: application/json).
  - `500 Internal Server Error` (Erro no servidor).

## 🧪 Testes (Curl & Postman)
- `curl -i URL` – teste rápido GET no terminal.
- `curl -X POST URL -H "Content-Type: application/json" -d '{"key":"value"}'` – POST com JSON.
- `curl -X PUT URL -H "Content-Type: application/json" -d '{"key":"value"}'` – PUT.
- `curl -X DELETE URL` – DELETE.
- `/health` – rota comum para verificar se API está viva.


═══════════════════════════════════════════════════════════════
DOCKER - CONTAINERIZAÇÃO
═══════════════════════════════════════════════════════════════

DOCKERFILE ESTRUTURA BASE
─────────────────────────────────────────────────────────────
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
ENV FLASK_APP=app.py
EXPOSE 5000
CMD ["python", "app.py"]


CONCEITOS ESSENCIAIS
─────────────────────────────────────────────────────────────
• Imagem: Template read-only com o código + dependências
• Contentor: Instância executável da imagem (isolada e efémera)
• Port mapping: -p 5000:5000 liga porta do host à porta do contentor
• Detached mode: -d corre em background, liberta o terminal


COMANDOS FUNDAMENTAIS
─────────────────────────────────────────────────────────────
Build da imagem:
  docker build -t nome-imagem .

Correr contentor (foreground):
  docker run -p 5000:5000 nome-imagem

Correr em background:
  docker run -d -p 5000:5000 --name meu-contentor nome-imagem

Ver contentores ativos:
  docker ps

Ver todos os contentores:
  docker ps -a

Ver logs:
  docker logs <container_id>
  docker logs -f <container_id>  # Logs em tempo real

Parar contentor:
  docker stop <container_id>

Remover contentor:
  docker rm <container_id>

Remover imagem:
  docker rmi <image_id>

Executar comando dentro do contentor:
  docker exec -it <container_id> bash

Limpar tudo (cuidado!):
  docker system prune -af


FLASK + DOCKER - CONFIGURAÇÃO CRÍTICA
─────────────────────────────────────────────────────────────
• app.run(host='0.0.0.0') obrigatório para acesso fora do contentor
• debug=True apenas em desenvolvimento (warnings sobre segurança)
• EXPOSE 5000 documenta a porta (não a abre automaticamente)


BOAS PRÁTICAS APLICADAS
─────────────────────────────────────────────────────────────
• Imagem slim: reduz tamanho e superfície de ataque
• --no-cache-dir no pip: reduz tamanho das camadas
• .dockerignore: excluir venv, __pycache__, .git
• WORKDIR absoluto: /app para clareza
• COPY requirements.txt primeiro: aproveita cache de layers


TROUBLESHOOTING WSL
─────────────────────────────────────────────────────────────
Problema: "docker: command not found" no WSL

Solução:
1. Abrir Docker Desktop no Windows
2. Settings → Resources → WSL Integration
3. Ativar "Enable integration with my default WSL distro"
4. Ativar toggle da distro Ubuntu
5. Apply & restart
6. No PowerShell: wsl --shutdown
7. Reabrir WSL: wsl


WORKFLOW TÍPICO
─────────────────────────────────────────────────────────────
1. Criar Dockerfile na raiz do projeto
2. Build: docker build -t minha-api .
3. Run: docker run -d -p 5000:5000 --name api-container minha-api
4. Testar: http://localhost:5000
5. Ver logs: docker logs api-container
6. Parar: docker stop api-container
7. Remover: docker rm api-container


PRÓXIMOS NÍVEIS
─────────────────────────────────────────────────────────────
• Docker Compose: orquestrar múltiplos contentores
• Multi-stage builds: otimizar tamanho da imagem
• Volumes: persistir dados fora do contentor
• Networks: comunicação entre contentores
• Docker Hub: partilhar imagens
• Gunicorn: servidor WSGI para produção


═══════════════════════════════════════════════════════════════
🐳 DOCKER COMPOSE - ORQUESTRAÇÃO
═══════════════════════════════════════════════════════════════

CONCEITO
─────────────────────────────────────────────────────────────
Ferramenta para definir e correr aplicações multi-contentor
usando ficheiros YAML. Um comando gere todo o ciclo de vida.


ESTRUTURA docker-compose.yml BASE
─────────────────────────────────────────────────────────────
version: '3.8'

services:
  web:
    build: .
    container_name: projeto1-flask-web
    ports:
      - "5000:5000"
    environment:
      - FLASK_ENV=development
    restart: unless-stopped


ESTRUTURA COM POSTGRESQL
─────────────────────────────────────────────────────────────
version: '3.8'

services:
  web:
    build: .
    container_name: projeto1-flask-web
    ports:
      - "5000:5000"
    environment:
      - DATABASE_URL=postgresql://postgres:senha@db:5432/tarefas_db
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15-alpine
    container_name: projeto1-flask-db
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=senha
      - POSTGRES_DB=tarefas_db
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

volumes:
  postgres_data:


COMANDOS ESSENCIAIS
─────────────────────────────────────────────────────────────
docker compose up              Build + criar + iniciar (foreground)
docker compose up -d           Correr em background (detached)
docker compose up --build      Rebuild após mudanças no código
docker compose down            Parar e remover contentores
docker compose down -v         Parar e remover contentores + volumes (limpa BD!)
docker compose logs -f         Ver logs em tempo real
docker compose logs -f web     Ver logs apenas do serviço web
docker compose ps              Ver status dos serviços
docker compose restart         Reiniciar serviços
docker compose restart web     Reiniciar apenas serviço web
docker compose stop            Parar sem remover
docker compose exec web bash   Executar comando no contentor


ESTRUTURA .dockerignore
─────────────────────────────────────────────────────────────
# Python
__pycache__/
*.pyc
venv/
*.db

# IDE
.vscode/
.idea/

# Git
.git/
.gitignore

# Docker
docker-compose.yml
Dockerfile


VANTAGENS
─────────────────────────────────────────────────────────────
• Um comando vs múltiplos (docker run, build, etc)
• Configuração versionada (YAML no Git)
• Networks automáticas entre serviços
• Fácil adicionar serviços (DB, Redis, etc)
• Ambiente reproduzível em qualquer máquina
• Volumes geridos automaticamente


COMPARAÇÃO: docker run vs docker compose
─────────────────────────────────────────────────────────────
ANTES (docker run):
  docker build -t projeto1-flask .
  docker run -d -p 5000:5000 --name minha-api projeto1-flask
  docker ps
  docker logs minha-api

AGORA (docker compose):
  docker compose up -d
  docker compose ps
  docker compose logs -f


TROUBLESHOOTING COMUM
─────────────────────────────────────────────────────────────
• "port already in use": Parar outros serviços na mesma porta
• "database does not exist": Verificar POSTGRES_DB no docker-compose.yml
• "404 Not Found" na API: Verificar se db.create_all() está no if __name__
• Mudanças não aplicadas: Usar docker compose up --build
• BD vazia após restart: Não usar down -v (apaga volumes!)


═══════════════════════════════════════════════════════════════
🗄️ POSTGRESQL - BASE DE DADOS
═══════════════════════════════════════════════════════════════

ACESSO À BD (DENTRO DO CONTENTOR)
─────────────────────────────────────────────────────────────
# Entrar no contentor
docker exec -it projeto1-flask-db psql -U postgres -d tarefas_db

# Comandos SQL úteis
\l                    # Listar bases de dados
\dt                   # Listar tabelas
\d tarefas            # Ver estrutura da tabela tarefas
\du                   # Listar utilizadores
\q                    # Sair do psql

# Queries básicas
SELECT * FROM tarefas;
SELECT * FROM tarefas WHERE concluida = true;
DELETE FROM tarefas WHERE id = 1;
DROP TABLE tarefas;   # Cuidado!


REDE & DIAGNÓSTICO
─────────────────────────────────────────────────────────────
# Ver IP do WSL (para Postman no Windows)
hostname -I

# Ver portas em uso
netstat -tuln | grep 5000
lsof -i :5000

# Testar conexão à BD
docker compose exec db psql -U postgres -c "SELECT version();"


ATALHOS BASH (ADICIONAR AO ~/.bashrc)
─────────────────────────────────────────────────────────────
# Git rápido
alias gs='git status'
alias ga='git add .'
alias gc='git commit -m'
alias gp='git push'
alias gl='git log --oneline'

# Docker rápido
alias dps='docker ps'
alias dcu='docker compose up'
alias dcud='docker compose up -d'
alias dcd='docker compose down'
alias dcl='docker compose logs -f'
alias dcb='docker compose up --build'

# Navegação
alias proj='cd ~/projetos'
alias flask1='cd ~/projetos/projeto1_flask'
alias ll='ls -lah'
alias ..='cd ..'

# Aplicar mudanças ao .bashrc
source ~/.bashrc


PRÓXIMOS PASSOS
─────────────────────────────────────────────────────────────
• Environment variables por ficheiro .env
• Health checks nos serviços
• Migrations com Alembic/Flask-Migrate
• Backup automático da BD
• Deploy (Render, Railway, Heroku)
• CI/CD com GitHub Actions
