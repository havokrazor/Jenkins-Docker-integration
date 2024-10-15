#A simple jenkins pipeline to verify if the docker slave configuration is working as expected.

pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
