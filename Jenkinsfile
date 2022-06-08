pipeline {
    // 스테이지 별로 다른 거
    agent any
    stages {
        // 레포지토리를 다운로드 받음
        stage('Prepare') {
            agent any
            
            steps {
                echo 'Clonning Repository'

                git url: 'https://github.com/wkemrm/jenkins-test.git',
                    branch: 'main',
                    credentialsId: '91b6606f-b9b2-400c-9b55-515c367e83fd'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    echo 'Successfully Cloned Repository'
                }

                always {
                  echo "i tried..."
                }

                cleanup {
                  echo "after all other post condition"
                }
            }
        }
        
        stage('Build Backend') {
          agent any
          steps {
            echo 'Build Backend'

            dir ('./backend'){
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
          }

          post {
            success {
              echo 'Successfully Cloned Repository'
            }
            failure {
              error 'This pipeline stops here...'
            }
          }
        }

        stage('build image Backend') {
          agent any
          steps {
            echo 'build image Backend'

            dir ('./backend') {
                sh 'docker build -t wkemrm12/docker-backend ./'
            }
          }

          post {
            success {
              echo 'Successfully Cloned Repository'
            }
            failure {
              error 'This pipeline stops here...'
            }
          }
        }

    }
}
