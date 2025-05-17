pipeline {
  environment {
    dockerimagename = "rohit19aug/pythonproject:v1.0.0"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
         git branch: 'main', url: 'https://github.com/rohituser/Python-Hello-World.git'
   }
  }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', 'DockerHub-Credential' ) {
          dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "kubectl apply -f k8s-and-docker.yaml")
        }
      }
    }
  }
}
