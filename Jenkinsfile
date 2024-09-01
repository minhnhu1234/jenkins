pipeline {
    agent any
    
    environment {
        // Define any environment variables here, if necessary
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example of using Maven to build
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example of running tests with Maven
                sh 'mvn test'
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
                // Example using SonarQube
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Example using OWASP Dependency-Check
                sh 'mvn dependency-check:check'
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
                // Example deployment command (e.g., using AWS CLI)
                sh 'aws deploy start-deployment --application-name MyApp --deployment-group-name StagingGroup --s3-location bucket=my-bucket,key=my-app.zip'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example of running tests on the staging environment
                sh 'mvn integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Example deployment command (e.g., using AWS CLI)
                sh 'aws deploy start-deployment --application-name MyApp --deployment-group-name ProductionGroup --s3-location bucket=my-bucket,key=my-app.zip'
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
