pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Забираем код из GitHub...'
                checkout scm
            }
        }
        stage('Check Files') {
            steps {
                echo '📄 Проверяем созданные файлы...'
                sh '''
                    ls -la
                    [ -f Dockerfile ] && echo "Dockerfile найден" || echo "Dockerfile не найден"
                    [ -f requirements.txt ] && echo "requirements.txt найден" || echo "requirements.txt не найден"
                    [ -d src ] && echo "Папка src найдена" || echo "Папка src не найдена"
                    [ -f src/app.py ] && echo "Файл src/app.py найден" || echo "Файл src/app.py не найден"
                    [ -f .dockerignore ] && echo ".dockerignore найден" || echo ".dockerignore не найден"
                '''
            }
        }
        stage('Docker Theory') {
            steps {
                echo 'ТЕОРИЯ DOCKER'
                echo 'docker build -t my-app .'
                echo 'docker run -d -p 8081:5000 my-app'
                echo 'curl http://localhost:8081/health'
            }
        }
        stage('Try Docker Commands') {
            steps {
                script {
                    try {
                        sh 'docker --version || echo "Docker не доступен"'
                        sh 'docker build -t test-image . 2>/dev/null || echo "Не удалось собрать образ"'
                    } catch (Exception e) {
                        echo "Docker команды не работают, нормально"
                    }
                }
            }
        }
    }

    post {
        always {
            echo '=== ИТОГ РАБОТЫ ==='
        }
        success {
            echo 'ОТЛИЧНО! CI/CD пайплайн түсінікті!'
        }
        failure {
            echo 'Были ошибки, тексеру керек!'
        }
    }
}
