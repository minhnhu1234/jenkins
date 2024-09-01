pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'minhnhu171202@gmail.com'  // Replace with the actual email address
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Build the application.'
                echo 'Tool: Maven'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit and integration tests.'
                echo 'Tool: Maven (JUnit for unit tests)'
            }
            post {
                always {
                        mail to: "${EMAIL_RECIPIENT}",
                        subject: "Jenkins Pipeline: Unit and Integration Tests - ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}. Check the attached logs for details.",
                        recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                        attachLog: true
                    
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
                always {
                        mail to: "${EMAIL_RECIPIENT}",
                        subject: "Jenkins Pipeline: Security Scan - ${currentBuild.currentResult}",
                        body: "The Security Scan stage has ${currentBuild.currentResult}. Check the attached logs for details.",
                        recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                        attachLog: true
                    
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

