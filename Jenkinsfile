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
                    mail to: 's220620441@deakin.edu.au',
                         subject: "Pipeline - Unit and Integration Tests Stage: ${currentBuild.currentResult}",
                         body: "The Unit and Integration Tests stage has finished with status: ${currentBuild.currentResult}",
                         attachLog: true
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
                    mail to: 's220620441@deakin.edu.au',
                         subject: "Pipeline - Security Scan Stage: ${currentBuild.currentResult}",
                         body: "The Security Scan stage has finished with status: ${currentBuild.currentResult}",
                         attachLog: true
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
    
    post {
        always {
            mail to: 's220620441@deakin.edu.au',
                 subject: "Pipeline Overall Status: ${currentBuild.currentResult}",
                 body: "The entire pipeline has finished with status: ${currentBuild.currentResult}",
                 attachLog: true
        }
    }
}
