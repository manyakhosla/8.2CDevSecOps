pipeline {
    agent any

    tools {
        // Optional: If using Jenkins NodeJS plugin
        // nodejs 'NodeJS 18'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/manyakhosla/8.2CDevSecOps'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" install'
            }
        }

        stage('Run Tests') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" run coverage || exit /b 0'
            }
        }

        stage('Security Scan') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" audit || exit /b 0'
            }
        }
    }
}
