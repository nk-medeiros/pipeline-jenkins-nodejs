pipeline {
    agent any

    stages {
        stage('Instalar Dependências') {
            steps {
                echo 'Instalando dependências do projeto Node.js...'
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Executando etapa de Build...'
                bat 'npm run build --if-present'
            }
        }

        stage('Teste') {
            steps {
                echo 'Executando testes...'
                bat 'npm test'
            }
        }
    }

    post {
        success {
            echo '====================================='
            echo ' Pipeline executado com SUCESSO! '
            echo '====================================='
        }
        failure {
            echo '====================================='
            echo ' Pipeline FALHOU! Verifique os erros. '
            echo '====================================='
        }
    }
}
