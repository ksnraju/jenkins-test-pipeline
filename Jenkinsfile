pipeline{
  agent any
  environment{
    REPO="docker.io/ksnraju/test-pipeline"
    REGISTRY_CREDENTIAL = "docker-hub-token-2"
  }
  stages{
    stage('Build'){
      steps{
        echo 'Building...'
        script{
          customImage = docker.build("${REPO}:${env.BUILD_ID}")
        }
        
      }
    }
    stage('Test'){
      steps{
        echo 'Testing...'
      }
    }
    stage('Deploy'){
      steps{
        echo 'Deploying...'
        script{
          docker.withRegistry('',"${REGISTRY_CREDENTIAL}"){
            customImage.push()
          }
        }
      }
    }
    stage('Clean Up'){
      steps{
        sh "docker rmi $REPO:$BUILD_NUMBER"
      }
    }
  }
}
