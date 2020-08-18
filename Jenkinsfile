pipeline {
  agent any
  stages {
    stage('检出'){
      steps {
        echo '构建中...'
      }
    }
    stage('构建') {
      steps {
        echo '构建中...'
        echo '构建完成.'
      }
    }
    stage('测试') {
      parallel {
        stage('单元测试') {
          steps {
            shell 'pwd' 
          }
        }
        stage('接口测试') {
          steps {
            echo '接口测试中...'
            echo '接口测试完成.'
          }
        }
      }
    }
  }
}
