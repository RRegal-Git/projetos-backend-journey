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
