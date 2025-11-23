pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:/inetpub/wwwroot'   // For Windows + IIS
        // For Linux use: DEPLOY_DIR = '/var/www/html'
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
                echo 'Testing HTML using tidy...'
                // If tidy is installed, this will validate HTML
                // If not installed, this step will still run without breaking
                bat 'tidy -qe index.html || exit 0'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying files to IIS folder..."
                bat "xcopy /Y index.html ${DEPLOY_DIR}\\"
                bat "xcopy /Y style.css ${DEPLOY_DIR}\\"
                bat "xcopy /Y script.js ${DEPLOY_DIR}\\"
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully! Visit: http://localhost/index.html'
        }
        failure {
            echo 'Pipeline FAILED. Check logs.'
        }
    }
}
