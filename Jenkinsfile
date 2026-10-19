pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '.venv/bin/python -m unittest discover -s .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    mkdir -p "$WORKSPACE/python-app-deploy"
                    cp app.py requirements.txt "$WORKSPACE/python-app-deploy/"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for more details.'
        }
    }
}