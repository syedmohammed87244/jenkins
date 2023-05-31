pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        // Use Maven to build the code
        sh 'mvn clean package'
      }
    }
    stage('Unit and Integration Tests') {
      steps {
        // Use JUnit to run unit tests
        sh 'mvn test'

        // Use Selenium to run integration tests
        // Assumes the tests are in the 'tests' directory
        sh 'selenium-runner run tests/'
      }
    }
    stage('Code Analysis') {
      steps {
        // Integrate SonarQube to analyze the code
        withSonarQubeEnv('SonarQube') {
          sh 'mvn sonar:sonar'
        }
      }
    }
    stage('Security Scan') {
      steps {
        // Perform a security scan using OWASP ZAP
        sh 'zap.sh -cmd -quickurl http://localhost:8080 -quickprogress -outfile report.html'
      }
    }
    stage('Deploy to Staging') {
      steps {
        // Use Ansible to deploy the application to a staging server
        withCredentials([sshUserPrivateKey(credentialsId: 'staging-server-key', keyFileVariable: 'SSH_KEY_FILE', passphraseVariable: '', usernameVariable: 'SSH_USER')]) {
          sh 'ansible-playbook -i staging.inventory deploy.yml'
        }
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        // Use Selenium to run integration tests on the staging environment
        // Assumes the tests are in the 'tests' directory
        sh 'selenium-runner run tests/'
      }
    }
    stage('Deploy to Production') {
      steps {
        // Use Ansible to deploy the application to a production server
        withCredentials([sshUserPrivateKey(credentialsId: 'production-server-key', keyFileVariable: 'SSH_KEY_FILE', passphraseVariable: '', usernameVariable: 'SSH_USER')]) {
          sh 'ansible-playbook -i production.inventory deploy.yml'
        }
      }
    }
  }