pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Build stage started"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh './venv/bin/pytest'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy stage completed"
            }
        }
    }
}

