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
    stage('Deploy to Kubernetes') {
    steps {
        withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG_FILE')]) {
            sh '''
                export KUBECONFIG=$KUBECONFIG_FILE
                kubectl apply --validate=false -f k8s-and-docker.yaml
            '''
            }
      }
    }
  }
}
