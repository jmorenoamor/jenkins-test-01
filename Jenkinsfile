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

    stage('Build') {
        steps {
            sh 'python --version'
        }
    }

    stage('Notify') {
        sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="Notification from Jenkins"'
    }
}
