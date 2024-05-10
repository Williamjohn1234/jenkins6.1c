pipeline {
    agent any

    environment {
        // Define environment variables with specific details
        GITHUB_REPOSITORY = 'https://github.com/Williamjohn1234/jenkins6.1c.git'
        EMAIL_RECIPIENT = 'williamdawsonog@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                script {
                    git url: "${env.GITHUB_REPOSITORY}"
                }
                sh 'mvn clean package'
            }
            post {
                success {
                    emailext(
                        subject: "Build Stage Completed Successfully",
                        body: "The build stage completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Build Stage Failed",
                        body: "The build stage failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
            post {
                success {
                    emailext(
                        subject: "Testing Stage Completed Successfully",
                        body: "The testing stage completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Testing Stage Failed",
                        body: "The testing stage failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                sh 'mvn sonar:sonar'
            }
            post {
                success {
                    emailext(
                        subject: "Code Analysis Stage Completed Successfully",
                        body: "The code analysis stage completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Code Analysis Stage Failed",
                        body: "The code analysis stage failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
            post {
                success {
                    emailext(
                        subject: "Security Scan Completed Successfully",
                        body: "The security scan stage completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Security Scan Failed",
                        body: "The security scan stage failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                sh './deploy-staging.sh'
            }
            post {
                success {
                    emailext(
                        subject: "Staging Deployment Completed Successfully",
                        body: "The staging deployment stage completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Staging Deployment Failed",
                        body: "The staging deployment stage failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'mvn verify'
            }
            post {
                success {
                    emailext(
                        subject: "Integration Tests on Staging Completed Successfully",
                        body: "Integration tests on staging completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Integration Tests on Staging Failed",
                        body: "Integration tests on staging failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh './deploy-production.sh'
            }
            post {
                success {
                    emailext(
                        subject: "Production Deployment Completed Successfully",
                        body: "The production deployment stage completed successfully for build ${env.BUILD_NUMBER}.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
                failure {
                    emailext(
                        subject: "Production Deployment Failed",
                        body: "The production deployment stage failed for build ${env.BUILD_NUMBER}. Check the Jenkins console for more details.",
                        to: "${env.EMAIL_RECIPIENT}"
                    )
                }
            }
        }
    }

    post {
        always {
            echo 'Final pipeline steps completed.'
        }
    }
}
