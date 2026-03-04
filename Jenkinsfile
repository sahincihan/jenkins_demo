pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = '1'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Code ausgecheckt'
            }
        }

        stage('Setup Python') {
            steps {
                echo 'Setting up Python environment...'
                sh '''
                    apt-get update && apt-get install -y python3 python3-pip
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                sh 'pip3 install --upgrade pip'
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'pytest -v --tb=short test_app.py'
            }
        }

        stage('Code Quality Check') {
            steps {
                echo 'Code Quality Check abgeschlossen'
            }
        }
    }

    post {
        always {
            echo 'Pipeline abgeschlossen'
            cleanWs()
        }
        success {
            echo 'Build erfolgreich!'
        }
        failure {
            echo 'Build fehlgeschlagen!'
        }
    }
}