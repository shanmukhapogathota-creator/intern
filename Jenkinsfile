
pipeline {
    agent any

    stages {

        // Stage 1: Checkout source code from GitHub
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code downloaded from GitHub'
            }
        }

        // Stage 2: Validate required files
        stage('Validate') {
            steps {
                bat '''
                    if not exist index.html exit /b 1
                    if not exist Jenkinsfile exit /b 1
                    echo Required files found
                '''
            }
        }

        // Stage 3: Test the application
        stage('Test') {
            steps {
                bat '''
                    findstr /i /c:"Question Bank Management" index.html
                    if errorlevel 1 exit /b 1
                    echo Application test passed
                '''
            }
        }

        // Stage 4: Build the application
        stage('Build') {
            steps {
                echo 'Static HTML application is ready to deploy'
            }
        }

        // Stage 5: Deploy the application to IIS
        stage('Deploy') {
            steps {
                bat '''
                    if not exist "C:\\inetpub\\wwwroot\\question-bank" (
                        mkdir "C:\\inetpub\\wwwroot\\question-bank"
                    )

                    copy /Y index.html "C:\\inetpub\\wwwroot\\question-bank\\index.html"

                    echo Application deployed successfully
                '''
            }
        }
    }

    // Post-build actions
    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
