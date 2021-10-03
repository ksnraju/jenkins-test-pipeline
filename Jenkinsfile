pipeline{
  agent any
  environment{
    REPO="docker.io/ksnraju/test-pipeline"
    REGISTRY_CREDENTIAL = "docker-hub-ksnraju-jenkins-token"
  }
  stages{
    stage('Build'){
      steps{
        echo 'Building...'
        customImage = docker.build("${REPO}:${env.BUILD_ID}")
        
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
        docker.withRegistry('',"${REGISTRY_CREDENTIAL}"){
          customImage.push()
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