# Bíblia de Comandos Linux

## Essenciais (sempre usar)
- `Tab` – autocomplete.
- `↑↓` – histórico comandos.
- `clear` – limpar terminal.

## Navegação
- `cd <pasta>` – mudar de diretório.
- `cd ~` – ir para o diretório home do utilizador.
- `pwd` – mostrar o diretório atual.

## Pastas e ficheiros
- `mkdir <nome>` – criar diretório.
- `ls` – listar conteúdo do diretório atual.
- `touch <nome>` – criar ficheiro vazio (ou atualizar timestamp).
- `code .` – abrir VS Code na pasta atual (quando o PATH estiver configurado).

## WSL (Windows + Linux)
- `wsl` – abrir Ubuntu a partir do PowerShell Windows.

## Ver ficheiros
- `cat ficheiro` – mostrar conteúdo no terminal.
- `head -10 ficheiro` – ver primeiras 10 linhas.
- `tail -10 ficheiro` – ver últimas 10 linhas.

## Copiar, mover, apagar
- `cp origem destino` – copiar ficheiro.
- `mv origem destino` – mover ou renomear ficheiro.
- `rm ficheiro` – apagar ficheiro (sem lixo!).

## Python no terminal
- `python3 ficheiro.py` – correr script Python.

## Editar ficheiros (terminal)
- `echo "texto" >> ficheiro` – adicionar texto ao final.

## Git básico
- `git init` – iniciar repositório local.
- `git status` – ver estado dos ficheiros.
- `git add .` – adicionar todos ficheiros.
- `git commit -m "msg"` – salvar snapshot.
- `git remote add origin URL` – ligar ao GitHub.
- `git push -u origin main` – enviar para GitHub.
- `git branch -M main` – renomear branch para main.
- `git log --oneline` – ver histórico commits.

## Python Virtual Environments (venv)
- `python3 -m venv venv` – criar ambiente virtual.
- `source venv/bin/activate` – ativar ambiente (prompt muda).
- `deactivate` – sair do ambiente.

## Pacotes Python (pip)
- `pip install nome_pacote` – instalar biblioteca.
- `pip install -r requirements.txt` – instalar lista de dependências.

## Controlar Processos
- `Ctrl+C` – parar servidor ou script que está a correr.

## Git ignore (repo limpo)
- `.gitignore` – ficheiro que diz ao Git quais pastas/ficheiros **não** devem ser versionados (ex.: `venv/`, `__pycache__/`). 
- `cat .gitignore` – ver conteúdo do `.gitignore` no terminal. 

## Remover ficheiros já versionados (sem apagar local)
- `git rm -r --cached venv` – deixa de versionar a pasta `venv/` (remove do “índice” do Git), mas mantém a pasta no teu computador. 
- Nota: adicionar ao `.gitignore` não remove o que já estava versionado; para isso usa-se `git rm --cached`. 

## Flask (melhorias de API)
- `/health` – endpoint simples para verificar se a API está viva (útil para monitorização e testes rápidos). 
- `@app.errorhandler(404)` – define um handler para devolver erro 404 em JSON (em vez de HTML), tornando a API consistente. 

## Testar API no terminal
- `curl -i http://127.0.0.1:5000/health` – testa a rota de saúde e mostra headers + status code. 
- `curl -i http://127.0.0.1:5000/rota_inventada` – confirma 404 a devolver JSON. 
## API & HTTP (Métodos)
- `GET` – pedir dados (padrão do browser/curl).
- `POST` – enviar dados para o servidor (criar/processar).
- `curl -X POST -H "Content-Type: application/json" -d '{"chave":"valor"}' URL` – enviar JSON via terminal.
- `415 Unsupported Media Type` – erro comum quando o cabeçalho Content-Type está mal escrito ou em falta.

### Git - Credenciais
- **Guardar password/token para não pedir sempre:**
  `git config --global credential.helper store`
  *(Pede uma última vez no próximo push e depois guarda para sempre)*

