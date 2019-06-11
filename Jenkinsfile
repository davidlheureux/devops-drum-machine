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
            sh 'sudo docker run -d --name student1 -p 7878:80 -p 2222:22 iliyan/docker-nginx-sshd & sudo usermod -a -G docker $USER'
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
