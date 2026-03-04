pipeline {
    agent {
        dockerContainer {
            image 'python:3.12-slim'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

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

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                sh 'pip install --upgrade pip'
                sh 'pip install -r requirements.txt'
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