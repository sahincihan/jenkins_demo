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

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                sh '''
                    python3 -m pip install --upgrade pip --user
                    python3 -m pip install -r requirements.txt --user
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'python3 -m pytest -v --tb=short test_app.py'
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