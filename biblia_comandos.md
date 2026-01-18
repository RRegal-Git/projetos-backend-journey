# Bíblia de Comandos Linux & Backend

## ⚡ Essenciais
- `Tab` – autocomplete (completa nomes de ficheiros/comandos).
- `↑↓` – histórico de comandos usados anteriormente.
- `clear` – limpar o ecrã do terminal.
- `Ctrl+C` – parar servidor ou script que está a correr.

## 📂 Navegação
- `cd <pasta>` – mudar de diretório.
- `cd ~` – ir para o diretório home (raiz do utilizador).
- `pwd` – mostrar o caminho da pasta atual.
- `ls` – listar ficheiros da pasta atual.
- `wsl` – abrir Ubuntu a partir do PowerShell Windows.

## 📄 Gestão de Ficheiros
- `mkdir <nome>` – criar diretório (pasta).
- `touch <nome>` – criar ficheiro vazio.
- `code .` – abrir VS Code na pasta atual.
- `cat ficheiro` – ler conteúdo no terminal.
- `echo "texto" >> ficheiro` – adicionar texto ao final de um ficheiro.
- `cp origem destino` – copiar ficheiro.
- `mv origem destino` – mover ou renomear ficheiro.
- `rm ficheiro` – apagar ficheiro (cuidado: não vai para a reciclagem!).

## 🐍 Python & Ambiente
- `python3 ficheiro.py` – correr script Python.
- `python3 -m venv venv` – criar ambiente virtual.
- `source venv/bin/activate` – ativar ambiente (essencial!).
- `deactivate` – sair do ambiente.

## 📦 Pacotes (Pip)
- `pip install nome_pacote` – instalar biblioteca (ex: Flask).
- `pip freeze > requirements.txt` – gerar lista de dependências instaladas ("congelar" versões).
- `pip install -r requirements.txt` – instalar dependências a partir de um ficheiro.

## 🐙 Git & GitHub
- `git init` – iniciar repositório novo.
- `git status` – ver o que mudou.
- `git add .` – preparar tudo para guardar.
- `git commit -m "msg"` – gravar snapshot (histórico).
- `git push` – enviar alterações para o GitHub.
- `git log --oneline` – ver histórico de commits resumido.
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

## 🧪 Testes (Curl & Postman)
- `curl -i URL` – teste rápido GET no terminal.
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

Parar contentor:
  docker stop <container_id>

Remover contentor:
  docker rm <container_id>

Remover imagem:
  docker rmi <image_id>


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


ESTRUTURA docker-compose.yml
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


COMANDOS ESSENCIAIS
─────────────────────────────────────────────────────────────
docker compose up              Build + criar + iniciar (foreground)
docker compose up -d           Correr em background (detached)
docker compose down            Parar e remover contentores
docker compose logs -f         Ver logs em tempo real
docker compose ps              Ver status dos serviços
docker compose up --build      Rebuild após mudanças no código
docker compose restart         Reiniciar serviços
docker compose stop            Parar sem remover


ESTRUTURA .dockerignore
─────────────────────────────────────────────────────────────
# Python
__pycache__/
*.pyc
venv/

# IDE
.vscode/
.idea/

# Git
.git/
.gitignore

# Docker
docker-compose.yml


VANTAGENS
─────────────────────────────────────────────────────────────
• Um comando vs múltiplos (docker run, build, etc)
• Configuração versionada (YAML no Git)
• Networks automáticas entre serviços
• Fácil adicionar serviços (DB, Redis, etc)
• Ambiente reproduzível em qualquer máquina


COMPARAÇÃO: docker run vs docker compose
─────────────────────────────────────────────────────────────
ANTES (docker run):
  docker build -t projeto1-flask .
  docker run -d -p 5000:5000 --name minha-api projeto1-flask
  docker ps
  docker logs minha-api

AGORA (docker compose):
  docker compose up


PRÓXIMOS PASSOS
─────────────────────────────────────────────────────────────
• Adicionar PostgreSQL ao docker-compose.yml
• Configurar volumes para persistência
• Environment variables por ficheiro .env
• Health checks nos serviços
