pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot\\'   // FIXED Windows IIS path
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                git branch: 'main', url: 'https://github.com/piyushm04/simple-web-ci-cd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Step: Listing workspace files'
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo 'Skipping tidy test (not installed on Windows)'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying files to IIS folder..."

                bat "copy /Y index.html ${DEPLOY_DIR}"
                bat "copy /Y style.css ${DEPLOY_DIR}"
                bat "copy /Y script.js ${DEPLOY_DIR}"
            }
        }
    }

    post {
        success {
            echo 'Deployment SUCCESS! Open: http://localhost/index.html'
        }
        failure {
            echo 'Pipeline FAILED. Check logs.'
        }
    }
}
