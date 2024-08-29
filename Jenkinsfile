pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'gn601800@gmail.com'
        BUILD_LOG_FILE = 'build-log.txt'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build' | tee "${BUILD_LOG_FILE}"
                echo 'Compiling and packaging the code...' | tee -a "${BUILD_LOG_FILE}"
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests' | tee -a "${BUILD_LOG_FILE}"
                echo 'Running unit and integration tests...' | tee -a "${BUILD_LOG_FILE}"
            }
            post {
                always {
                    script {
                        archiveArtifacts artifacts: "${BUILD_LOG_FILE}", excludes: ''
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Jenkins Pipeline: Unit and Integration Tests Stage - ${currentBuild.currentResult}",
                             body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}.",
                             attachmentsPattern: "${BUILD_LOG_FILE}"
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis' | tee -a "${BUILD_LOG_FILE}"
                echo 'Analyzing the code quality...' | tee -a "${BUILD_LOG_FILE}"
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan' | tee -a "${BUILD_LOG_FILE}"
                echo 'Performing security scan...' | tee -a "${BUILD_LOG_FILE}"
            }
            post {
                always {
                    script {
                        archiveArtifacts artifacts: "${BUILD_LOG_FILE}", excludes: ''
                        mail to: "${env.EMAIL_RECIPIENT}",
                             subject: "Jenkins Pipeline: Security Scan Stage - ${currentBuild.currentResult}",
                             body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}.",
                             attachmentsPattern: "${BUILD_LOG_FILE}"
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging' | tee -a "${BUILD_LOG_FILE}"
                echo 'Deploying the application to the staging environment...' | tee -a "${BUILD_LOG_FILE}"
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging' | tee -a "${BUILD_LOG_FILE}"
                echo 'Running integration tests on the staging environment...' | tee -a "${BUILD_LOG_FILE}"
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production' | tee -a "${BUILD_LOG_FILE}"
                echo 'Deploying the application to the production environment...' | tee -a "${BUILD_LOG_FILE}"
            }
        }
    }
    
    post {
        always {
            script {
                archiveArtifacts artifacts: "${BUILD_LOG_FILE}", excludes: ''
                mail to: "${env.EMAIL_RECIPIENT}",
                     subject: "Jenkins Pipeline: ${currentBuild.currentResult} - ${env.JOB_NAME}",
                     body: "The pipeline has completed with status: ${currentBuild.currentResult}.",
                     attachmentsPattern: "${BUILD_LOG_FILE}"
            }
        }
    }
}
