pipeline {
  agent {
    dockerContainer {
      image 'python:3.12-slim'
      args '-u root:root'
    }
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Install') {
      steps { sh 'pip install -r requirements.txt' }
    }

    stage('Test') {
      steps { sh 'pytest -q' }
    }
  }
}