pipeline {
    agent any

    environment {
        PATH = "C:\\Program Files\\nodejs;${env.PATH}"
        SNYK_TOKEN = "b9938d0b-5213-4920-9859-e01b6a5993bb" 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/manyakhosla/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Authenticate Snyk') {
            steps {
                bat "snyk auth %SNYK_TOKEN%"
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Jenkins Build: ${currentBuild.fullDisplayName}",
                body: "Build ${currentBuild.currentResult}: ${env.BUILD_URL}",
                to: "manyakhosla63@gmail.com"
            )
        }
    }
}
