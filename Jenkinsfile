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
                pip install pymssql
                pip install pyodbc
                pytest test_file.py
                '''
                echo 'Python tests have been run.'
            }
        }
    }
}