pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests using JUnit'
            }
            post {
                always {
                    emailext (
                        subject: 'Unit and Integration Tests Status',
                        to: 'syed87244@gmail.com',
                        body: "Unit and Integration Tests completed SUCCESSFULLY.",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        subject: 'Unit and Integration Tests Status',
                        to: 'syed87244@gmail.com',
                        body: 'Failure! Please check logs.',
                        attachLog: true
                    )
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
                echo 'Performing a security scan on the code using OWASP ZAP'
            }
            post {
                always {
                    emailext (
                        subject: 'Security Scan Status',
                        to: 'syed87244@gmail.com',
                        body: "Security Scan completed SUCCESSFULLY.",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        subject: 'Security Scan Status',
                        to: 'syed87244@gmail.com',
                        body: 'Failure! Please check the logs.',
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to an AWS EC2.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment using Selenium'
            }
            post {
                always {
                    emailext (
                        subject: 'Integration Tests on Staging Status',
                        to: 'syed87244@gmail.com',
                        body: "Integration Tests on Staging completed SUCCESSFULLY.",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        subject: 'Integration Tests on Staging Status',
                        to: 'syed87244@gmail.com',
                        body: 'Failure! Please check the logs.',
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to an AWS.'
            }
        }
    }
}
