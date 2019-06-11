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
            sh label:'stop docker student1', 'sudo docker stop student1'
            sh label:'rm docker sudent1', 'sudo docker rm student1'
            sh label:'run docker', 'sudo docker run -d --name student1 -p 8008:80 -p 2222:22 iliyan/docker-nginx-sshd'
            sh label:'copy file 1','sudo docker cp "public/index.html" "student1:sites/"'
            sh label:'copy file 2','sudo docker cp "public/app" "student1:sites/app"'
            sh label:'copy file 1','sudo docker cp "public/assets" "student1:sites/assets"'
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
        sh 'sudo curl localhost:8008'
      }
    }
    
     
  }
}
