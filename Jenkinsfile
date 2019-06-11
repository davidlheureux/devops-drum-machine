pipeline {
  agent any 
  stages {
    stage('Compile') {
      agent any
      steps {
        sh 'sudo npm install'
        sh 'sudo npm run-script build'
      }
    }
    stage('Unit Testing') {
      agent any
      steps {
        sh 'sudo npm run-script test'
      }
    }
    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            echo 'allo'
          }
        }
        stage('Archive Artifacts') {
          steps {
            archiveArtifacts 'public/'
          }
        }
      }
    }
    stage('Integration testing') {
      steps {
        sleep 10
        sh 'sudo curl localhost'
      }
    }
  }
}
