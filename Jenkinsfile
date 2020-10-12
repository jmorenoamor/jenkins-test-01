pipeline {
    agent {
        docker {
            image 'python:3.5.1'
        }
    }

    environment {
        PROJECT_NAME = "Jenkins Test"
        TOKEN_ID = credentials('HULK_NOTIFIER_TOKEN_ID')
        ID = credentials('HULK_NOTIFIER_ID')
    }

    stages {
        stage('Build') {
            steps {
                sh script: 'python --version', label: "Version"
            }
        }

        stage('Notify') {
            steps {
                // sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${JOB_NAME} [${BUILD_NUMBER}] (${BUILD_URL})"'
                // sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${GIT_COMMIT} [${GIT_URL}] (${GIT_BRANCH})"'
                // sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN_ID}/sendMessage -d chat_id=${ID} -d text="${RUN_DISPLAY_URL} [${RUN_CHANGES_DISPLAY_URL}] (${JOB_DISPLAY_URL})"'
                //  --data-urlencode "text=[Detail](${RUN_DISPLAY_URL}) \n BRANCH_NAME=${BRANCH_NAME} \n CHANGE_ID=${CHANGE_ID} \n CHANGE_URL=${CHANGE_URL} \n CHANGE_TITLE=${CHANGE_TITLE} \n CHANGE_AUTHOR=${CHANGE_AUTHOR} \n CHANGE_AUTHOR_DISPLAY_NAME=${CHANGE_AUTHOR_DISPLAY_NAME} \n CHANGE_AUTHOR_EMAIL=${CHANGE_AUTHOR_EMAIL} \n CHANGE_TARGET=${CHANGE_TARGET} \n CHANGE_BRANCH=${CHANGE_BRANCH} \n CHANGE_FORK=${CHANGE_FORK} \n TAG_NAME=${TAG_NAME} \n TAG_TIMESTAMP=${TAG_TIMESTAMP} \n TAG_UNIXTIME=${TAG_UNIXTIME} \n TAG_DATE=${TAG_DATE} \n BUILD_NUMBER=${BUILD_NUMBER} \n BUILD_ID=${BUILD_ID} \n BUILD_DISPLAY_NAME=${BUILD_DISPLAY_NAME} \n JOB_NAME=${JOB_NAME} \n JOB_BASE_NAME=${JOB_BASE_NAME} \n BUILD_TAG=${BUILD_TAG} \n EXECUTOR_NUMBER=${EXECUTOR_NUMBER} \n NODE_NAME=${NODE_NAME} \n NODE_LABELS=${NODE_LABELS} \n WORKSPACE=${WORKSPACE} \n WORKSPACE_TMP=${WORKSPACE_TMP} \n JENKINS_HOME=${JENKINS_HOME} \n JENKINS_URL=${JENKINS_URL} \n BUILD_URL=${BUILD_URL} \n JOB_URL=${JOB_URL} \n GIT_COMMIT=${GIT_COMMIT} \n GIT_PREVIOUS_COMMIT=${GIT_PREVIOUS_COMMIT} \n GIT_PREVIOUS_SUCCESSFUL_COMMIT=${GIT_PREVIOUS_SUCCESSFUL_COMMIT} \n GIT_BRANCH=${GIT_BRANCH} \n GIT_LOCAL_BRANCH=${GIT_LOCAL_BRANCH} \n GIT_CHECKOUT_DIR=${GIT_CHECKOUT_DIR} \n GIT_URL=${GIT_URL} \n GIT_COMMITTER_NAME=${GIT_COMMITTER_NAME} \n GIT_AUTHOR_NAME=${GIT_AUTHOR_NAME} \n GIT_COMMITTER_EMAIL=${GIT_COMMITTER_EMAIL} \n GIT_AUTHOR_EMAIL=${GIT_AUTHOR_EMAIL} \n MERCURIAL_REVISION=${MERCURIAL_REVISION} \n MERCURIAL_REVISION_SHORT=${MERCURIAL_REVISION_SHORT} \n MERCURIAL_REVISION_NUMBER=${MERCURIAL_REVISION_NUMBER} \n MERCURIAL_REVISION_BRANCH=${MERCURIAL_REVISION_BRANCH} \n MERCURIAL_REPOSITORY_URL=${MERCURIAL_REPOSITORY_URL} \n SVN_REVISION=${SVN_REVISION} \n SVN_URL=${SVN_URL}" \
                sh script: '''
                    curl -X "POST" "https://api.telegram.org/bot${TOKEN_ID}/sendMessage" \
                         -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
                         --data-urlencode "text=✅ *$PROJECT_NAME* \n\n Successful built branch [$BRANCH_NAME](${GIT_URL.replace('.git', '')}/tree/$BRANCH_NAME) \n Job details [Detail]($RUN_DISPLAY_URL)" \
                         --data-urlencode "chat_id=${ID}" \
                         --data-urlencode "disable_web_page_preview=true" \
                         --data-urlencode "parse_mode=markdown"
                ''', label: "Notify"
            }
        }
    }
}
