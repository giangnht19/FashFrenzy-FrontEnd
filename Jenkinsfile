pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'gn601800@gmail.com'
        BUILD_LOG_FILE = 'build-log.txt'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    def buildOutput = 'Stage 1: Build\nCompiling and packaging the code...'
                    echo buildOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: buildOutput
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    def testOutput = 'Stage 2: Unit and Integration Tests\nRunning unit and integration tests...'
                    echo testOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: testOutput, append: true
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: "${BUILD_LOG_FILE}"
                    emailext attachmentsPattern: "${BUILD_LOG_FILE}",
                             to: "${env.EMAIL_RECIPIENT}",
                             subject: "Jenkins Pipeline: Unit and Integration Tests Stage - ${currentBuild.currentResult}",
                             body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}."
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    def codeAnalysisOutput = 'Stage 3: Code Analysis\nAnalyzing the code quality...'
                    echo codeAnalysisOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: codeAnalysisOutput, append: true
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    def securityScanOutput = 'Stage 4: Security Scan\nPerforming security scan...'
                    echo securityScanOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: securityScanOutput, append: true
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: "${BUILD_LOG_FILE}"
                    emailext attachmentsPattern: "${BUILD_LOG_FILE}",
                             to: "${env.EMAIL_RECIPIENT}",
                             subject: "Jenkins Pipeline: Security Scan Stage - ${currentBuild.currentResult}",
                             body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}."
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    def deployOutput = 'Stage 5: Deploy to Staging\nDeploying the application to the staging environment...'
                    echo deployOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: deployOutput, append: true
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    def integrationTestsOutput = 'Stage 6: Integration Tests on Staging\nRunning integration tests on the staging environment...'
                    echo integrationTestsOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: integrationTestsOutput, append: true
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    def productionDeployOutput = 'Stage 7: Deploy to Production\nDeploying the application to the production environment...'
                    echo productionDeployOutput
                    writeFile file: "${BUILD_LOG_FILE}", text: productionDeployOutput, append: true
                }
            }
        }
    }
    
    post {
        script {
            def pipelineOutput = "Success"
            echo pipelineOutput
            writeFile file : "${BUILD_LOG_FILE}", text: pipelineOutput, append: true
        }
        always {
            archiveArtifacts artifacts: "${BUILD_LOG_FILE}"
            emailext attachmentsPattern: "${BUILD_LOG_FILE}",
                     to: "${env.EMAIL_RECIPIENT}",
                     subject: "Jenkins Pipeline: ${currentBuild.currentResult} - ${env.JOB_NAME}",
                     body: "The pipeline has completed with status: ${currentBuild.currentResult}."
        }
    }
}
