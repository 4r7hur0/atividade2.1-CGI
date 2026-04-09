# Atividade 2.1 — Mini Blog (Flask + CSV)

Página de blog em Python usando Flask, com:
- envio de mensagens (autor + mensagem)
- registro de data/hora do envio
- persistência em arquivo `CSV` lido/escrito pelo app

## Estrutura
- `app.py`: aplicação Flask
- `templates/index.html`: página (form + listagem)
- `data/messages.csv`: arquivo gerado automaticamente com `author,message,created_at`

## Como rodar (Windows / PowerShell)
Entre na pasta do projeto:

```powershell
cd C:\laragon\www\ahhh\atividade2.1
```

Crie e ative um ambiente virtual:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Instale as dependências:

```powershell
pip install -r requirements.txt
```

Rode o servidor:

```powershell
python .\app.py
```

Acesse:
- `http://127.0.0.1:5000/`

## Deploy no Render
### Subir no GitHub
- Faça commit da pasta `atividade2.1` e suba para um repositório no GitHub.

### Criar o serviço no Render
- No Render, crie um **Web Service** a partir do repositório.
- Aponte o **Root Directory** para `atividade2.1` (ou deixe na raiz e ajuste os comandos).
- Comandos:
  - **Build Command**: `pip install -r requirements.txt`
  - **Start Command**: `gunicorn app:app --bind 0.0.0.0:$PORT`

Você também pode usar o arquivo `render.yaml` deste projeto.

### Persistência do CSV (importante)
Este app grava em `data/messages.csv`.
- Em plano Free no Render, o disco pode ser **efêmero** (o arquivo pode sumir em restart/redeploy).
- Se você precisa que continue registrando “pra sempre”, use um **Persistent Disk** no Render e ajuste o app
  para gravar no mount path do disco (ex.: `/var/data/messages.csv`) ou migre para banco (Render Postgres/SQLite em disco persistente).

## Como apresentar em sala (roteiro rápido)
- Abrir a página no navegador.
- Enviar uma mensagem.
- Mostrar que o arquivo `data/messages.csv` foi criado/atualizado com autor/mensagem/data.
- Mostrar rapidamente no `app.py`:
  - rotas `GET /` e `POST /`
  - leitura/escrita do CSV
  - redirect pós-POST (evita duplicar ao dar refresh)

