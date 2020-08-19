pipeline {
  agent any
 stages {	
     stage('代码质量检查') {
      parallel {
        
        stage('单元测试') {
          steps {
            echo '接口测试中...'
            echo '接口测试完成.'
          }
        }
      }
    }
    
    stage('自动化验收测试') {
      parallel {
       
        stage('冒烟测试') {
          steps {
            echo '接口测试中...'
            echo '接口测试完成.'
          }
        }
      }
    }
    
    stage('打包镜像'){
      steps {
        echo '构建中...'
      }
    } 
    
    
    stage('推送项目制品库'){
      steps {
        echo '构建.'
      }
    }
      
    
  }
}
