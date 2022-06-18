 pipeline {
 
 
  agent any
   
    environment{
        VERSION = "${env.BUILD_ID}"
        IMAGE_NAME = "yannickeboo/anael"
    }
    stages {
          
        stage('Build') { 
            agent { 
              docker { image 'docker.io/library/maven:3-openjdk-18-slim' }
          }
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
     stage('docker image') {
      
      steps {
       
       withDockerRegistry([ credentialsId: "Docker_hub", url: "https://index.docker.io/v1/" ]) {
       sh 'docker build . -t $IMAGE_NAME:app1-$VERSION -f account-service/Dockerfile'
       sh 'docker tag $IMAGE_NAME:app1-$VERSION $IMAGE_NAME:$VERSION'
       sh 'docker push $IMAGE_NAME:app1-$VERSION'
       sh 'docker push $IMAGE_NAME:$VERSION'
        
        }
       
        
     
         
      }
     }
    }
}

