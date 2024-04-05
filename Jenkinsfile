pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    DOCKER_HUB_LOGIN_USR = credentials('docker_hub_user')
    DOCKER_HUB_LOGIN_PSW = credentials('docker_hub_pass')
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
          mv Dockerfile webapp
          mv package.json webapp
          mv package-lock.json webapp
          mv sum.js webapp
          cd webapp
          docker build -t testapp .
          '''       
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW
        docker tag testapp kellykjd/testapp:latest
        docker push kellykjd/testapp:latest   
        '''
        }
      }
    }
}


    
  

