# Deploy Flask na AWS Elastic Beanstalk (Padrão Theron)

Este guia foi feito para repetir o mesmo processo em outras verticais.

## 1) AWS CLI - `aws configure`

Quando rodar `aws configure`, use:

- AWS Access Key ID: sua chave
- AWS Secret Access Key: sua chave secreta
- Default region name: ex. `us-east-1` (ou a região padrão da Theron)
- Default output format: `json`

Resposta curta para sua dúvida: sim, o mais comum é `json`.

## 2) Pré-requisitos do projeto Flask

Na raiz do projeto, garanta:

- `requirements.txt` com `Flask` e `gunicorn`
- `Procfile` com:

```txt
web: gunicorn app:app
```

- `.ebignore` para não enviar lixo para o deploy:

```txt
venv/
.git/
__pycache__/
*.pyc
.DS_Store
```

## 3) Instalar EB CLI

```powershell
pip install awsebcli --upgrade
```

## 4) Inicializar Elastic Beanstalk

Na raiz do projeto:

```powershell
eb init
```

Escolhas recomendadas:

- Região: padrão da empresa (ex. `us-east-1`)
- Plataforma: Python 3.x
- CodeCommit: `No` (se não usar)
- SSH setup: `Yes` se quiser acessar instância por SSH, senão `No`

## 5) Criar ambiente (primeiro deploy)

```powershell
eb create NOME-DO-AMBIENTE
```

Exemplo:

```powershell
eb create theron-tour-prod
```

## 6) Publicar alterações

```powershell
eb deploy
```

Abrir no navegador:

```powershell
eb open
```

## 7) Comandos úteis do dia a dia

```powershell
eb status
eb logs
eb health
```

## 8) Variáveis de ambiente

```powershell
eb setenv FLASK_ENV=production CHAVE=valor
```

## 9) Padronização para próximas verticais

Troque apenas estes itens:

- Nome do repositório
- Nome do ambiente (`eb create ...`)
- Região (se necessário)
- Variáveis de ambiente específicas

Sugestão de naming:

- App: `theron-<vertical>`
- Ambiente prod: `theron-<vertical>-prod`
- Ambiente hml: `theron-<vertical>-hml`

## 10) Checklist rápido

- [ ] `requirements.txt` ok
- [ ] `Procfile` ok
- [ ] `.ebignore` ok
- [ ] `aws configure` feito com output `json`
- [ ] `eb init` concluído
- [ ] `eb create` concluído
- [ ] `eb deploy` com sucesso
- [ ] `eb open` funcionando

## 11) Template de execução (copiar e colar)

```powershell
# 1) Entrar na pasta do projeto
cd C:\caminho\do\projeto

# 2) (Opcional) Ativar venv
.\venv\Scripts\Activate.ps1

# 3) Garantir EB CLI
pip install awsebcli --upgrade

# 4) Configurar AWS (primeira vez na máquina)
aws configure
# default output: json

# 5) Inicializar app EB (primeira vez no projeto)
eb init

# 6) Criar ambiente (primeira vez no projeto)
eb create theron-vertical-prod

# 7) Deploy
eb deploy

# 8) Abrir aplicação
eb open
```
