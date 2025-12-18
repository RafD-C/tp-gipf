pipeline {
agent any
environment {
  SONAR_HOST_URL = '172.17.0.1'
  SONAR_TOKEN = 'sqp_edbedb5f1efc5084970cc98e3b4cea2762281165'
  }
stages {
  stage('Checkout') {
    steps {
    checkout scm
    }
  }
  
stage('Sonar') {
    steps {
      sh '''
./gradlew sonarqube
-Dsonar.projectKey=tp-gipf
-Dsonar.projectName='tp-gipf'
-Dsonar.host.url=${SONAR_HOST_URL}
-Dsonar.login=${SONAR_TOKEN}
'''
    }
  }
}
