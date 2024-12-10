pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'pytest tests/' // Ensure you have tests in a "tests" folder
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Azure...'
                withCredentials([string(credentialsId: 'AZURE_CREDENTIALS', variable: 'AZURE_CLI')]) {
                    sh 'az login --service-principal --username $APP_ID --password $PASSWORD --tenant $TENANT_ID'
                    sh 'func azure functionapp publish varun-hello-world-function
'
                }
            }
        }
    }
}
