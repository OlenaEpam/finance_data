pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                echo "Running ${env.BUILD_ID} ${env.BUILD_DISPLAY_NAME} on ${env.NODE_NAME} and JOB ${env.JOB_NAME}"
            }
        }
        stage('Test'){
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
        stage('Push') {
            steps {
                sshagent(['jenkins-ssh-key']) {
                    sh '''
                        git config --global user.name "OlenaEpam"
                        git config --global user.email "Olena_Pavlyushchik@epam.com"
                        git add -A
                        if [[ -n $(git status --porcelain) ]]; then
                            git commit -m "Add test results"
                            git push origin HEAD:main
                        fi
                    '''
                }
            }
        }
    }
}