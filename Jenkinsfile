pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Replace with your build command (e.g., make, npm build, etc.)
                sh 'your-build-command-here'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Replace with your test command
                sh 'your-test-command-here'
            }
            post {
                always {
                    // Send email notification
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
                // Replace with your code analysis command
                sh 'your-code-analysis-command-here'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Replace with your security scan command
                sh 'your-security-scan-command-here'
            }
            post {
                always {
                    // Send email notification
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
                // Replace with your deployment command
                sh 'your-deployment-command-here'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Replace with your staging integration test command
                sh 'your-staging-integration-test-command-here'
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
