pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]],
                                                                                                                                                                            userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }

    stage('编译') {
      steps {
        sh './mvnw package -Dmaven.test.skip=true'
      }
    }

    stage('单元测试') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }

      }
      steps {
        sh './mvnw test'
      }
    }

    stage('打包镜像') {
      steps {
        sh "docker build -t ${ARTIFACT_IMAGE}:${env.GIT_BUILD_REF} ."
        sh "docker tag ${ARTIFACT_IMAGE}:${env.GIT_BUILD_REF} ${ARTIFACT_IMAGE}:latest"
      }
    }

  }
  environment {
    ENTERPRISE = 'xunituandui'
    PROJECT = 'coding-demo'
    ARTIFACT = 'coding-demo'
    CODE_DEPOT = 'coding-demo'
    ARTIFACT_BASE = "${ENTERPRISE}-docker.pkg.coding.net"
    ARTIFACT_IMAGE = "${ARTIFACT_BASE}/${PROJECT}/${ARTIFACT}/${CODE_DEPOT}"
  }
  post {
    always {
      junit 'build/reports/**/*.xml'
    }

  }
  parameters {
    string(defaultValue: 'maintaner', description: '123', name: '456')
  }
}