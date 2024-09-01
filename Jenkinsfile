pipeline {
    agent any

    tools {
        maven 'M3' 
    }

    environment {
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
               
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
              
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
        
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
             
                sh 'mvn dependency-check:check'
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
             
                sh 'aws deploy start-deployment --application-name MyApp --deployment-group-name StagingGroup --s3-location bucket=my-bucket,key=my-app.zip'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
             
                sh 'mvn integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
               
                sh 'aws deploy start-deployment --application-name MyApp --deployment-group-name ProductionGroup --s3-location bucket=my-bucket,key=my-app.zip'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir() 
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}

