pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/seu-usuario/seu-repositorio'
            }
        }
        
        stage('Setup') {
            steps {
                sh 'pip install -r requirements.txt' // Instala as dependências
            }
        }
        
        stage('Start MySQL Container') {
            steps {
                sh 'docker run -d --name mysql-container -e MYSQL_ROOT_PASSWORD=examplepassword -e MYSQL_DATABASE=mydatabase -p 3306:3306 mysql:latest'
                sleep 30 // Espera algum tempo para o MySQL iniciar
            }
        }
        
        stage('Test') {
            steps {
                sh 'python -m pytest tests/test_app.py' // Executa os testes
            }
        }
    }

    post {
        always {
            // Limpar recursos, como o contêiner MySQL
            sh 'docker rm -f mysql-container'
        }
    }
}
