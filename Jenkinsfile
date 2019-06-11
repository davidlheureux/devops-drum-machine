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
            sh label: 'Docker run', returnStatus: false, script: 'sudo docker stop student1'
            sh label: 'Docker run', returnStatus: false, script: 'sudo docker rm student1'
            sh label: 'Docker run', returnStatus: true, script: 'sudo docker run -d --name student1 -p 7878:80 -p 2222:22 iliyan/docker-nginx-sshd'
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
