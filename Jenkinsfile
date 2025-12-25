pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'nileshkasurde11@gmail.com'
    }

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

    post {

        success {
            emailext(
                subject: "✅ Jenkins Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                Hello Team,

                Good news! 🎉

                Jenkins Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                Status: SUCCESS ✅

                Build URL:
                ${env.BUILD_URL}

                Regards,
                Jenkins
                """,
                to: "${EMAIL_RECIPIENT}"
            )
        }

        failure {
            emailext(
                subject: "❌ Jenkins Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                Hello Team,

                Unfortunately, the Jenkins build has FAILED ❌

                Jenkins Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                Status: FAILED

                Please check logs here:
                ${env.BUILD_URL}

                Regards,
                Jenkins
                """,
                to: "${EMAIL_RECIPIENT}"
            )
        }

        always {
            echo "Pipeline execution finished (success or failure)"
        }
    }
}

