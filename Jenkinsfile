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
              sh '''./gradlew sonar \
                    -Dsonar.projectKey=tp-gipf \
                    -Dsonar.projectName='tp-gipf' \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.token=sqp_edbedb5f1efc5084970cc98e3b4cea2762281165'''
          }
      }
      stage('Run Tests') {
          steps {
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 test'
          }
      }
    }
}
