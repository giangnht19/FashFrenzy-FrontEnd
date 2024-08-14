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
                script {
                    echo 'Stage 1: Build'
                    echo 'Task: Compile and package the code using a build automation tool.'
                    echo 'Tool: Maven'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Stage 2: Unit and Integration Tests'
                    echo 'Task: Run unit tests to verify code functionality and integration tests to ensure components work together.'
                    echo 'Tool: JUnit with Maven'
                }
            }
            post {
                always {
                    script {
                        def logContent = currentBuild.rawBuild.getLog()
                        writeFile file: 'unit_integration_tests.log', text: logContent.join("\n")
                    }
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Jenkins Pipeline: Unit and Integration Tests Stage - ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}.",
                        attachLog: true,
                        attachmentsPattern: 'unit_integration_tests.log'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Stage 3: Code Analysis'
                    echo 'Task: Analyze the code to ensure it meets industry standards.'
                    echo 'Tool: SonarQube'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Stage 4: Security Scan'
                    echo 'Task: Perform a security scan to identify any vulnerabilities in the code.'
                    echo 'Tool: OWASP Dependency Check'
                }
            }
            post {
                always {
                    script {
                        def logContent = currentBuild.rawBuild.getLog()
                        writeFile file: 'security_scan.log', text: logContent.join("\n")
                    }
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Jenkins Pipeline: Security Scan Stage - ${currentBuild.currentResult}",
                        body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}.",
                        attachLog: true,
                        attachmentsPattern: 'security_scan.log'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Stage 5: Deploy to Staging'
                    echo 'Task: Deploy the application to a staging server for further testing.'
                    echo 'Tool: AWS CLI for EC2 deployment'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Stage 6: Integration Tests on Staging'
                    echo 'Task: Run integration tests in the staging environment to ensure production-like functionality.'
                    echo 'Tool: Selenium for UI tests'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Stage 7: Deploy to Production'
                    echo 'Task: Deploy the application to the production environment.'
                    echo 'Tool: Kubernetes for container orchestration'
                }
            }
        }
    }
}
