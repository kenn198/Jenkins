pipeline {
	agent any
	    tools {
        maven 'Maven' // The name of the Maven installation in Jenkins configuration
    }
        environment {
        DIRECTORY_PATH = 'C:\\path\\to\\your\\project'
        EMAIL_RECIPIENT = 's223342348@deakin.edu.au'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the project using Maven.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium.'
            }
            post {
                always {
                    emailext (
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Test Stage Completed - ${currentBuild.fullDisplayName}",
                        body: """<p>Test stage completed.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>""",
                        attachmentsPattern: "**/target/surefire-reports/*.xml",
                        mimeType: 'text/html'
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality with SonarQube.'
            }
        }
        stage('Security Scan') {
        steps {
            echo 'Performing security scanning using OWASP ZAP.'
        }
        post {
            always {
                emailext (
                    to: "${env.EMAIL_RECIPIENT}",
                    subject: "Security Scan Stage Completed - ${currentBuild.fullDisplayName}",
                    body: """<p>Security scan stage completed.</p>
                                <p>Status: ${currentBuild.currentResult}</p>""",
                    attachmentsPattern: "**/security-reports/*.json",
                    mimeType: 'text/html'
                )
            }
        }
    }
    stage('Deploy to Staging') {
        steps {
            echo 'Deploying application to staging environment on AWS EC2.'
        }
    }
    stage('Integration Tests on Staging') {
        steps {
            echo 'Running integration tests on staging environment using Selenium.'
        }
    }
    stage('Deploy to Production') {
        steps {
            echo 'Deploying application to production environment on AWS EC2.'
        }
    }
}
    post {
        failure {
                always {
                    emailext (
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Build Stage Fail - ${currentBuild.fullDisplayName}",
                        body: """<p>Build stage Failed.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>""",
                        attachmentsPattern: "**/target/surefire-reports/*.xml",
                        mimeType: 'text/html'
                    )
                }
        }
        success {
            echo 'Pipeline completed successfully.'
        }
    }
}