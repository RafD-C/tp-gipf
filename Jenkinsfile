pipeline {
agent any
environment {
  SONAR_HOST_URL = '172.17.0.1'
  SONAR_TOKEN = 'sqp_ef018e086b27be928451b420b11f0667a38e0642'
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
