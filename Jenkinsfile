pipeline {
    agent any
    
    environment {
        GITHUB_REPOSITORY = 'https://github.com/Williamjohn1234/jenkins6.1c.git'
        EMAIL_RECIPIENT = 'williamjohnson00007@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from the repo: ${GITHUB_REPOSITORY}"
                echo "Building the code using Maven"
            }
            post {
                always {
                    emailext (
                        subject: "Build Stage Status: ${currentBuild.result}",
                        body: "The build stage of the pipeline has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit"
                echo "Running integration tests using Selenium"
            }
            post {
                always {
                    emailext (
                        subject: "Test Stage Status: ${currentBuild.result}",
                        body: "The test stage of the pipeline has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Analyzing the code using SonarQube"
            }
            post {
                always {
                    emailext (
                        subject: "Code Analysis Stage Status: ${currentBuild.result}",
                        body: "The code analysis stage of the pipeline has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing a security scan on the code using OWASP ZAP"
            }
            post {
                always {
                    emailext (
                        subject: "Security Scan Stage Status: ${currentBuild.result}",
                        body: "The security scan stage of the pipeline has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to a staging server using AWS CodeDeploy"
                echo "Using AWS CodeDeploy to deploy the application to an EC2 instance"
            }
            post {
                always {
                    emailext (
                        subject: "Deploy to Staging Stage Status: ${currentBuild.result}",
                        body: "The deploy to staging stage has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment using Selenium"
            }
            post {
                always {
                    emailext (
                        subject: "Integration Tests on Staging Status: ${currentBuild.result}",
                        body: "Staging integration tests stage has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to a production server using AWS CodeDeploy"
                echo "Using AWS CodeDeploy to deploy the application to an EC2 instance"
            }
            post {
                always {
                    emailext (
                        subject: "Deploy to Production Stage Status: ${currentBuild.result}",
                        body: "The deploy to production stage has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
    }
}
