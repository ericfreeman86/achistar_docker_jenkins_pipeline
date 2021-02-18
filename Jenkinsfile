pipeline {
  environment {
    registry = "ericfreeman86/achistar_docker_jenkins_pipeline"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', 'dockerhub' ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}

node {
    stage('Execute Image'){
        def customImage = docker.build("ericfreeman86/achistar_docker_jenkins_pipeline:${env.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo Hello'
        }
    }
}
