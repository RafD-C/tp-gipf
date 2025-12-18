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
  
stage('Build') {
    steps {
      sh './gradlew build -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128'
    }
  }
  stage('SonarQube Analysis') {
    steps {
      withCredentials([string(credentialsId: 'tp-gipf', variable: 'SONAR_TOKEN')]) {
      withSonarQubeEnv('SonarQube') {
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
  }
}

  post {
    always {
      junit '/src/test/java/gipf//.xml'
      archiveArtifacts artifacts: '**/build/libs/.jar', allowEmptyArchive: true
    }
  }  
}
