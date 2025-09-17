pipeline {
    agent any

    environment {
        DOTNET_ROOT = "C:\\Program Files\\dotnet"
        PATH = "${env.DOTNET_ROOT};${env.PATH}"  // Include dotnet in PATH if needed
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/manish8778/MyDotNetApp.git'
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Publish') {
            steps {
                bat 'dotnet publish -c Release -o output'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add deployment commands here, e.g., copying files or restarting services
            }
        }
		
		stage('Commit and Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-creds-id', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                    bat '''
                        git config --global user.email "manish_8778@yahoo.com"
                        git config --global user.name "Manish Shende"
                        git add .
                        git commit -m "Automated commit from Jenkins"
                        git push https://%GIT_USER%:%GIT_PASS%@github.com/manish8778/MyDotNetApp.git master
                    '''
                }
            } // close steps
        } // close stage 'Commit and Push'
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
