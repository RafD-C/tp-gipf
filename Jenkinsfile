pipeline {
  agent any
  stages {
      stage('Checkout') {
          steps {
              git branch: 'master', url: 'https://github.com/RafD-C/tp-gipf'
          }
      }
      stage('Build') {
          steps {
            sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 compileJava'
          }
      }
    stage('Test') {
          steps {
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 test'
          }
      }
      stage('Sonar') {
          steps {
              sh '''./gradlew sonar \
                    -Dhttps.proxyHost="proxy1-rech" \
                    -Dhttps.proxyPort=3128 compileJava\
                    -Dsonar.projectKey=tp-gipf \
                    -Dsonar.projectName='tp-gipf' \
                    -Dsonar.host.url=http://127.17.0.1:9000 \
                    -Dsonar.token=sqp_7103d07193bbe2fe90e629211ab8cdfa7222c141
                    '''
          }
      }
    stage('Jar') {
          steps {
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 jar'
          }
      }
    stage('Release') {
        steps {
            archiveArtifacts artifacts: 'build/libs/**/*.jar'
        }
    }
    }
}
