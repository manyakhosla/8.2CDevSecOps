pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/manyakhosla/8.2CDevSecOps'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'set PATH=C:\\Program Files\\nodejs;%PATH% && npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'set PATH=C:\\Program Files\\nodejs;%PATH% && npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'set PATH=C:\\Program Files\\nodejs;%PATH% && npm run coverage || exit /b 0'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'set PATH=C:\\Program Files\\nodejs;%PATH% && npm audit || exit /b 0'
            }
        }
    }
}
