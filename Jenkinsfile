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
            post {
                success {
                    emailext to: 'manyakhosla63@gmail.com',
                        subject: 'Run Tests Stage: SUCCESS',
                        body: 'Run tests stage completed successfully.',
                        attachLog: true
                }
                failure {
                    emailext to: 'alfithomas13@gmail.com',
                        subject: 'Run Tests Stage: FAILURE',
                        body: 'Run tests stage failed.',
                        attachLog: true
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'set PATH=C:\\Program Files\\nodejs;%PATH% && npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'set PATH=C:\\Program Files\\nodejs;%PATH% && npm audit || exit /b 0'
            }
            post {
                success {
                    emailext to: 'manyakhosla63@gmail.com',
                        subject: 'Security Scan: SUCCESS',
                        body: 'Security scan completed successfully.',
                        attachLog: true
                }
                failure {
                    emailext to: 'manyakhosla63@gmail.com',
                        subject: 'Security Scan: FAILURE',
                        body: 'Security scan failed.',
                        attachLog: true
                }
            }
        }
    }
}
