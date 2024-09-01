pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'minhnhu171202@gmail.com'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'npm test'
            }
            post {
                always {
                    emailext (
                        subject: "Unit and Integration Tests: ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests have ${currentBuild.currentResult}. Check the logs for more details.",
                        recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                // Example: Using ESLint for JavaScript projects
                sh 'npm run lint'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Example: Using npm audit for security scanning
                sh 'npm audit'
            }
            post {
                always {
                    emailext (
                        subject: "Security Scan: ${currentBuild.currentResult}",
                        body: "The Security Scan has ${currentBuild.currentResult}. Check the logs for more details.",
                        recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Replace with your deployment command (e.g., using AWS CLI or another tool)
                sh 'your-deployment-command-here'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'npm run integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Replace with your production deployment command
                sh 'your-production-deployment-command-here'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir() // clean up the workspace
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
