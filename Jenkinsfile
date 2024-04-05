pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
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
        docker tag testapp giank8/testapp:latest
        docker push giank8/testapp:latest   
        '''
        }
      }
    }
}
  

