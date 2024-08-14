pipeline {
    agent any

    environment {
        DIRECTORY_PATH = 'C:\\Users\\gn213\\OneDrive\\Tài liệu\\GitHub\\FashFrenzy-FrontEnd'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'Edward Nguyen'  // Replace 'your_name' with your actual name
        EMAIL_RECIPIENT = 'gn601800@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests using JUnit'
                echo 'Running integration tests using Selenium'
            }
            post {
                success {
                    script {
                        archiveArtifacts artifacts: '**/*', excludes: ''
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Unit and Integration Tests Passed",
                             body: "Unit and integration tests passed successfully.",
                             attachmentsPattern: 'archive/**/*.log'
                    }
                }
                failure {
                    script {
                        archiveArtifacts artifacts: '**/*', excludes: ''
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Unit and Integration Tests Failed",
                             body: "Unit and integration tests failed. Please check the Jenkins console output for more details.",
                             attachmentsPattern: 'archive/**/*.log'
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code using SonarQube'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
            }
            post {
                success {
                    script {
                        archiveArtifacts artifacts: '**/*', excludes: ''
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Security Scan Passed",
                             body: "Security scan passed successfully.",
                             attachmentsPattern: 'archive/**/*.log'
                    }
                }
                failure {
                    script {
                        archiveArtifacts artifacts: '**/*', excludes: ''
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Security Scan Failed",
                             body: "Security scan failed. Please check the Jenkins console output for more details.",
                             attachmentsPattern: 'archive/**/*.log'
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to staging server using Jenkins Deploy Plugin'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment using Selenium Grid'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production server using Jenkins Deploy Plugin'
            }
        }
    }
    
    post {
        success {
            script {
                archiveArtifacts artifacts: '**/*', excludes: ''
                mail to: "${env.EMAIL_RECIPIENT}",
                     subject: "Build Status Email",
                     body: "Build succeeded.",
                     attachmentsPattern: 'archive/**/*.log'
            }
        }
        failure {
            script {
                archiveArtifacts artifacts: '**/*', excludes: ''
                mail to: "${env.EMAIL_RECIPIENT}",
                     subject: "Build Failed",
                     body: "The build has failed. Please check the Jenkins console output for more details.",
                     attachmentsPattern: 'archive/**/*.log'
            }
        }
    }
}
