pipeline {
  agent any 
  stages {
    stage('Compile') {
      agent any
      steps {
        sh 'npm install'
        sh 'npm run-script build'
      }
    }
    stage('Unit Testing') {
      agent any
      steps {
        sh 'npm run-script test'
      }
    }
 
    stage('Free Infra') {
      steps {
        sh 'sudo docker stop student1'
        sh 'sudo docker rm student1'
      }
    }
    
  }
}
