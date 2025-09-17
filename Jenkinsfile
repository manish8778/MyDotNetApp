pipeline {
    agent any

    environment {
        DOTNET_ROOT = "C:\\Program Files\\dotnet"
    }
	

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/manish8778/MyDotNetApp.git'
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release'
            }
        }

        stage('Test') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish -c Release -o output'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add deployment commands here, e.g., copying files or restarting services
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
