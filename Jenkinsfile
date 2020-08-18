pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: env.GIT_BUILD_REF]],
        userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]])
      }
    }
    stage('并行阶段 2') {
      parallel {
        stage('代码质量检查') {
          steps {
            echo '构建中...'
            script {
              def exists = fileExists 'README.md'
              if (!exists) {
                writeFile(file: 'README.md', text: 'Helloworld')
              }
            }

            archiveArtifacts(artifacts: 'README.md', fingerprint: true)
            echo '构建完成.'
          }
        }
        stage('单元测试') {
          steps {
            echo '123'
          }
        }
      }
    }
    stage('测试') {
      parallel {
        stage('自动化验收测试') {
          steps {
            echo '单元测试中...'
            echo '单元测试完成.'
            writeFile(file: 'TEST-demo.junit4.AppTest.xml', text: '''
                        <testsuite name="demo.junit4.AppTest" time="0.053" tests="3" errors="0" skipped="0" failures="0">
                            <properties>
                            </properties>
                            <testcase name="testApp" classname="demo.junit4.AppTest" time="0.003"/>
                            <testcase name="test1" classname="demo.junit4.AppTest" time="0"/>
                            <testcase name="test2" classname="demo.junit4.AppTest" time="0"/>
                        </testsuite>
                    ''')
            junit '*.xml'
          }
        }
        stage('冒烟测试') {
          steps {
            echo '接口测试中...'
            echo '接口测试完成.'
          }
        }
      }
    }
    stage('打包镜像') {
      steps {
        sh 'echo hello CODING'
      }
    }
    stage('推送项目制品库') {
      steps {
        sh 'echo hello CODING'
      }
    }
  }
}
