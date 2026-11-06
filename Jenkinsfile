
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code downloaded from GitHub'
            }
        }

        stage('Validate') {
            steps {
                bat '''
                    if not exist index.html exit /b 1
                    if not exist Jenkinsfile exit /b 1
                    echo Required files found
                '''
            }
        }

        stage('Test') {
            steps {
                bat '''
                    findstr /i /c:"Question Bank Management" index.html
                    if errorlevel 1 exit /b 1
                    echo Application test passed
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Static HTML application is ready to deploy'
            }
        }
    }
    
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


    post {
        success {
            echo 'CI pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
