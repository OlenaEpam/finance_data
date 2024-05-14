pipeline {
    agent any

    stages {
        stage('Test') {
            steps{
                sh '''
                python3 -m venv env
                . env/bin/activate
                pip install pytest
                pip install sqlalchemy
                pip install pyodbc
                pytest test_file_trial.py
                '''
                echo 'Python tests have been run.'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['jenkins-ssh-key']) {
                    withCredentials([string(credentialsId: 'github-pat', variable: 'PAT')]) {
                        sh '''
                            git fetch origin develop:develop
                            if git show-ref --quiet refs/heads/release; then
                                git branch -D release
                            fi
                            git checkout -b release develop
                            git remote set-url origin https://$PAT@github.com/OlenaEpam/finance_data.git
                            git push origin release --force
                        '''
                        echo 'Code has been deployed.'
                    }
                }
            }
        }
    }
}