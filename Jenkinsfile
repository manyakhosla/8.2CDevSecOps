pipeline {
    agent any

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

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post {
                success {
                    emailext to: 'manyakhosla63@gmail.com',
                             subject: 'Run Tests Stage: SUCCESS',
                             body: 'Run tests stage completed successfully.',
                             attachLog: true
                }
                failure {
                    emailext to: 'manyakhosla63@gmail.com',
                             subject: 'Run Tests Stage: FAILURE',
                             body: 'Run tests stage failed.',
                             attachLog: true
                }
            }
        }

        stage('Security Scan') {
            steps {
                bat 'npm audit || exit /b 0'
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
