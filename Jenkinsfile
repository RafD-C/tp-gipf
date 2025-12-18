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
      stage('Run Sonarqube') {
          steps {
              sh './gradlew sonar \
                  -Dsonar.projectKey=tp \
                  -Dsonar.projectName="tp" \
                  -Dsonar.host.url=http://172.17.0.1:9000 \
                  -Dsonar.token=sqp_ce3212db5c33d3d53335643be75c6c724131602d'
          }
      }
      stage('Run Tests') {
          steps {
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 test'
          }
      }
    }
}
