pipeline {
  agent any

  tools {
    maven 'Maven3'    // name you configured in Jenkins
    jdk 'JDK17'       // optional, if you have a JDK tool configured
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build with Maven') {
      steps {
        sh 'mvn -version'
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        deploy adapters: [
          tomcat9(credentialsId: 'tomcat-credentials',
                  path: '',
                  url: 'http://54.74.253.1:8080')
        ],
        contextPath: '/sample',
        war: 'target/sample.war'
      }
    }
  }
}
