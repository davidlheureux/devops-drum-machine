pipeline {
  agent any 
  stages {
    stage('Compile') {
      agent any
      steps {
        sh 'npm install'
        sh 'npm run-script build'
        chuckNorris()
        stash includes:"public", name:'sitesFiles'
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
            //sh label:"stop docker student1", script:'sudo docker stop student1'
            //sh label:"rm docker sudent1", script:'sudo docker rm student1'
            //sh label:"run docker", script:'sudo docker run -d --name student1 -p 8008:80 -p 2222:22 iliyan/docker-nginx-sshd'
            //sh label:"copy file 1",script:'sudo docker cp "public/index.html" "student1:sites/"'
            //sh label:"copy rep2",script:'sudo docker cp "public/app" "student1:sites/app"'
            //sh label:"copy rep3",script:'sudo docker cp "public/assets" "student1:sites/assets"'
            unstash 'sitesFiles'
            sshPublisher(publishers: [sshPublisherDesc(configName: 'student1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'sites', remoteDirectorySDF: false, removePrefix: 'public', sourceFiles: 'public')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])            
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
