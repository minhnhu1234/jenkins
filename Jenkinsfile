pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'minhnhu171202@gmail.com'  
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Build the application.'
                echo 'Tool: Maven'
            }
            post {
                success {
                    mail to: "${EMAIL_RECIPIENT}",
                         subject: "Build Stage: Success",
                         body: "The Build stage was successful!"
                }
                failure {
                    mail to: "${EMAIL_RECIPIENT}",
                         subject: "Build Stage: Failure",
                         body: "The Build stage failed. Please check the logs for details."
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit and integration tests.'
                echo 'Tool: Maven (JUnit for unit tests)'
            }
            post {
                success {
                    mail to: "${EMAIL_RECIPIENT}",
                         subject: "Unit and Integration Tests Stage: Success",
                         body: "The Unit and Integration Tests stage was successful!"
                }
                failure {
                    mail to: "${EMAIL_RECIPIENT}",
                         subject: "Unit and Integration Tests Stage: Failure",
                         body: "The Unit and Integration Tests stage failed. Please check the logs for details."
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Task: Run code analysis.'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Task: Perform a security scan.'
                echo 'Tool: OWASP Dependency-Check'
            }
            post {
                success {
                    mail to: "${EMAIL_RECIPIENT}",
                         subject: "Security Scan Stage: Success",
                         body: "The Security Scan stage was successful!"
                }
                failure {
                    mail to: "${EMAIL_RECIPIENT}",
                         subject: "Security Scan Stage: Failure",
                         body: "The Security Scan stage failed. Please check the logs for details."
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Task: Deploy to staging environment.'
                echo 'Tool: AWS CLI'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run integration tests on staging.'
                echo 'Tool: Maven (JUnit for integration tests)'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Task: Deploy to production environment.'
                echo 'Tool: AWS CLI'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
