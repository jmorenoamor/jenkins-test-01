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
                // sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${JOB_NAME} [${BUILD_NUMBER}] (${BUILD_URL})"'
                // sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${GIT_COMMIT} [${GIT_URL}] (${GIT_BRANCH})"'
                // sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${RUN_DISPLAY_URL} [${RUN_CHANGES_DISPLAY_URL}] (${JOB_DISPLAY_URL})"'
                sh '''
                    curl -X "POST" "https://api.telegram.org/bot${TOKEN_ID}/sendMessage" \
                         -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
                         --data-urlencode "text=Successful build: [Detail](${RUN_DISPLAY_URL})" \
                         --data-urlencode "chat_id=${ID}" \
                         --data-urlencode "disable_web_page_preview=true" \
                         --data-urlencode "parse_mode=markdown"
                '''
            }
        }
    }
}
