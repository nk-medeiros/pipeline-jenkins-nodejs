# Pipeline Jenkins Node.js

Projeto Node.js utilizado para demonstrar um pipeline de CI/CD com Jenkins.

## Requisitos

* Node.js
* npm

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

O servidor será iniciado pelo arquivo `server.js`.

## Comandos disponíveis

```bash
npm install    # Instala as dependências
npm run build  # Executa o build
npm test       # Executa os testes
npm start      # Inicia a aplicação
```

## CI/CD Pipeline (GitHub Actions)

O projeto possui um workflow configurado no GitHub Actions (`.github/workflows/main.yml`) executando as etapas:

1. **Setup & Install:** Instalação das dependências com Node.js 18.
2. **SAST:** Análise estática de código com **Semgrep** (`p/javascript`).
3. **Build & Test:** Execução do build (`npm run build`) e testes unitários (`npm test`).
4. **DAST:** Análise dinâmica de segurança com **OWASP ZAP** rodando contra a aplicação na porta `3000`.