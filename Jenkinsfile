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
    
     stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh 'set +e'
            sh 'sudo docker stop student1'
            sh 'sudo docker rm student1'
            sh 'set -e'
            sh 'sudo docker run -d --name student1 -p 7878:80 -p 2222:22 iliyan/docker-nginx-sshd'
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
        sh 'sudo curl localhost:7878'
      }
    }
    
     
  }
}
