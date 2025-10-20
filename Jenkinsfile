pipeline { 
  agent any 
  environment { 
    IMAGE_NAME = 'ayaacvia/simple-app' 
    REGISTRY_CREDENTIALS = 'dockerhub-credentials' 
  } 
  stages { 
    stage('Checkout') { steps { checkout scm } } 
    stage('Build') { steps { bat 'echo "Build di Windows"' } } 
    stage('Build Docker Image') { steps { bat "docker build -t %IMAGE_NAME%:%BUILD_NUMBER% ." } } 
    stage('Push Docker Image') { 
      steps { 
        withCredentials([usernamePassword(credentialsId: REGISTRY_CREDENTIALS, usernameVariable: 'USER', passwordVariable: 'PASS')]) { 
          bat """ 
          docker login -u %USER% -p %PASS%
          docker push ayaacvia/simple-app
          """
        } 
      } 
    } 
  } 
}


