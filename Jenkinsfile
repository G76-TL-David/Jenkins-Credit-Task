pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Build tool: Maven
                // sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Test tool: JUnit
                // sh 'mvn test'
            }
            post {
                always {
                    script {
                        // Ensure the directory for the log file exists
                        def workspace = pwd()
                        def logFile = "${workspace}/unit_test_log.txt"

                        // Capture the log content
                        def logContent = currentBuild.rawBuild.getLog(50).join("\n")

                        // Write the log content to a file
                        writeFile file: logFile, text: logContent

                        // Ensure the log file was created successfully
                        if (fileExists(logFile)) {
                            // Send email with log file attached
                            emailext attachmentsPattern: 'unit_test_log.txt',
                                     to: 's220620441@deakin.edu.au',
                                     subject: "Pipeline - Unit and Integration Tests Stage: ${currentBuild.currentResult}",
                                     body: "The Unit and Integration Tests stage has finished with status: ${currentBuild.currentResult}. Please see the attached log file for details."
                        } else {
                            echo "Log file was not created, email will not include an attachment."
                        }
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // Code analysis tool: SonarQube
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Security scan tool: OWASP Dependency-Check
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    script {
                        // Ensure the directory for the log file exists
                        def workspace = pwd()
                        def logFile = "${workspace}/security_scan_log.txt"

                        // Capture the log content
                        def logContent = currentBuild.rawBuild.getLog(50).join("\n")

                        // Write the log content to a file
                        writeFile file: logFile, text: logContent

                        // Ensure the log file was created successfully
                        if (fileExists(logFile)) {
                            // Send email with log file attached
                            emailext attachmentsPattern: 'security_scan_log.txt',
                                     to: 's220620441@deakin.edu.au',
                                     subject: "Pipeline - Security Scan Stage: ${currentBuild.currentResult}",
                                     body: "The Security Scan stage has finished with status: ${currentBuild.currentResult}. Please see the attached log file for details."
                        } else {
                            echo "Log file was not created, email will not include an attachment."
                        }
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Deploy to a staging environment e.g., AWS EC2 instance
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Commands to run tests on the staging environment
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Deploy to a production environment e.g., AWS EC2 instance
            }
        }
    }
}
