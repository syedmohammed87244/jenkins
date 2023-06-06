pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        echo "building......"
      }
    }
    stage('Unit and Integration Tests') {
      steps {
        echo "test....."
      }
    }
    stage('Code Analysis') {
      steps {
        echo "code......."
      }
    }
    stage('Security Scan') {
      steps {
        echo "security scan..........."
      }
    }
    stage('Deploy to Staging') {
      steps {
        echo "deploying to staging..........."
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        echo "integrating tests........."
      }
    }
    stage('Deploy to Production') {
      steps {
        echo "Deploying........."
      }
    }
  }
  
  post {
    always {
      // Send notification emails at the end of test and security scan stages
      emailext body: "Pipeline ${currentBuild.result} - View logs: ${env.BUILD_URL}console",
        subject: "Pipeline ${currentBuild.result}: ${env.JOB_NAME}",
        to: "syed87244@gmail.com",
        attachmentsPattern: '**/*.log',
        attachLog: true
    }
  }
}
