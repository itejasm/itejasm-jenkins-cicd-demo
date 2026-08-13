pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                git branch: 'main',
                    url: 'https://github.com/itejasm/itejasm-jenkins-cicd-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Step: Checking project files...'
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo 'Test Step: Checking required files...'
                bat 'if not exist index.html exit /b 1'
                bat 'if not exist style.css exit /b 1'
                bat 'if not exist script.js exit /b 1'
                echo 'All required files are present.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying files to IIS...'
                bat "xcopy /Y /I * ${DEPLOY_DIR}\\"
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully!'
            echo 'Visit: http://localhost/index.html'
        }

        failure {
            echo 'Pipeline failed! Check build logs.'
        }
    }
}
