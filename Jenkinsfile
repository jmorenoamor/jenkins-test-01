pipeline {
    agent {
        docker {
            image 'python:3.5.1'
        }
    }

    environment {
        TOKEN_ID = credentials('HULK_NOTIFIER_TOKEN_ID')
        ID = credentials('HULK_NOTIFIER_ID')
    }

    stages {
        stage('Build') {
            steps {
                sh 'python --version'
            }
        }

        stage('Notify') {
            steps {
                sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${env.JOB_NAME} [${env.BUILD_NUMBER}] (${env.BUILD_URL})"'
            }
        }
    }
}
