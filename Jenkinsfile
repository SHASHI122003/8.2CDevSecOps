pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/SHASHI122003/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit Security Scan') {
            steps {
                sh 'npm audit || true'
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Jenkins Build Result: ${currentBuild.currentResult}",
                body: """
Build Status: ${currentBuild.currentResult}
Project: NodeGoofPipeline
Build Number: ${env.BUILD_NUMBER}
                """,
                to: "shashidhar1812@gmail.com",
                attachLog: true
            )
        }
    }
}
