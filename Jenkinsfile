pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning project from GitHub..."
                git branch: 'main', url: 'https://github.com/piyushm04/simple-web-ci-cd.git'
            }
        }

        stage('Build') {
            steps {
                echo "Build Step: Listing workspace files"
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo "Skipping tidy test (not installed on Windows)"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying files to IIS folder..."
                bat """
                copy /Y web-app\\index.html C:\\inetpub\\wwwroot\\
                copy /Y web-app\\script.js C:\\inetpub\\wwwroot\\
                copy /Y web-app\\style.css C:\\inetpub\\wwwroot\\
                """
            }
        }
    }

    post {
        failure {
            echo 'Pipeline FAILED. Check logs.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
    }
}
