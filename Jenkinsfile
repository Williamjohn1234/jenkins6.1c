pipeline {
    agent any
    
    environment {
        GITHUB_REPOSITORY = 'https://github.com/Williamjohn1234/jenkins6.1c.git'
        EMAIL_RECIPIENT = 'williamjohnson00007@gmail.com'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code from ${GITHUB_REPOSITORY}"
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                sh 'mvn clean install'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit"
                sh 'mvn test'
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
                sh 'mvn sonar:sonar'
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
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment using Selenium"
            }
            post {
                always {
                    emailext (
                        subject: "Integration Tests on Staging Status: ${currentBuild.result}",
                        body: "Staging Integration tests stage has completed with the following status: ${currentBuild.result}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to production using AWS CodeDeploy"
                echo "Using AWS CodeDeploy to deploy the application to an EC2 instance"
            }
        }
    }
}
