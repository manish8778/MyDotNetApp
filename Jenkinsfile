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
                withCredentials([usernamePassword(credentialsId: '388374f4-be64-4263-b710-b3baf7adeefe', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                    bat '''
                        echo This is a new file created by Jenkins > newfile.txt
                git config --global user.email "manish_8778@yahoo.com"
                git config --global user.name "Manish Shende"
                git add newfile.txt
                git commit -m "Add newfile.txt from Jenkins"
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
