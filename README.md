# Pipeline Jenkins Node.js

Projeto Node.js utilizado para demonstrar um pipeline de CI/CD com Jenkins e GitHub Actions, incluindo build de imagem com Docker e análises de segurança (SAST/DAST).

## Requisitos

- Node.js 18+
- npm
- Docker (opcional, para executar a aplicação em container)

## Instalação

Clone o repositório:

```bash
git clone <URL_DO_REPOSITORIO>
cd pipeline-jenkins-nodejs
```

Instale as dependências:

```bash
npm install
```

## Build

Execute o build:

```bash
npm run build
```

O comando apenas simula uma etapa de build e exibe uma mensagem de sucesso.

## Testes

Execute os testes automatizados:

```bash
npm test
```

Os testes utilizam **Jest** e **Supertest**.

## Execução

Inicie a aplicação:

```bash
npm start
```

O servidor será iniciado pelo arquivo `server.js` na porta `3000`.

## Docker

A aplicação pode ser executada em container usando o `Dockerfile` da raiz do projeto.

### O que o Dockerfile faz

1. Usa a imagem base leve `node:18-alpine`.
2. Define `/app` como diretório de trabalho.
3. Copia o `package.json` e o `package-lock.json` e instala apenas as dependências de produção com `npm ci --omit=dev`. Essa etapa vem antes da cópia do código para aproveitar o cache de camadas do Docker.
4. Copia o restante do código-fonte (os arquivos listados no `.dockerignore` são ignorados).
5. Expõe a porta `3000` e inicia a aplicação com `npm start`.

### Como usar

Construir a imagem:

```bash
docker build -t pipeline-jenkins-nodejs .
```

Executar o container:

```bash
docker run -d -p 3000:3000 --name pipeline-app pipeline-jenkins-nodejs
```

A aplicação ficará disponível em `http://localhost:3000`.

Parar e remover o container:

```bash
docker stop pipeline-app && docker rm pipeline-app
```

## Comandos disponíveis

```bash
npm install                                  # Instala as dependências
npm run build                                # Executa o build
npm test                                     # Executa os testes
npm start                                    # Inicia a aplicação
docker build -t pipeline-jenkins-nodejs .    # Constrói a imagem Docker
docker run -p 3000:3000 pipeline-jenkins-nodejs  # Executa o container
```

## CI/CD Pipeline (GitHub Actions)

O projeto possui um workflow configurado no GitHub Actions (`.github/workflows/main.yml`), executado a cada push e pull request nas branches `main` e `master`, com as etapas:

1. **Setup & Install:** instalação das dependências com Node.js 18 (`npm ci`).
2. **SAST:** análise estática de código com Semgrep (`p/javascript` e `p/nodejs`). O relatório é salvo como artifact (`relatorio-sast`).
3. **Build & Test:** execução do build (`npm run build`) e dos testes unitários (`npm test`).
4. **Docker Build:** construção da imagem Docker da aplicação e validação do container em execução na porta `3000`.
5. **DAST:** análise dinâmica de segurança com OWASP ZAP rodando contra o container. Os relatórios em HTML e JSON são salvos como artifact (`relatorio-dast`).
