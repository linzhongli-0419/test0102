pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        echo '111 222 333 444 555 666 777 888 999 12'
      }
    }

    stage('stage-2') {
      steps {
        sh './mvnw package -Dmaven.test.skip=true'
      }
    }

  }
}