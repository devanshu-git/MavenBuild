pipeline {
  agent any

  environment {
    TOMCAT_URL = 'http://192.168.10.50:8080'  // Tomcat base URL
    WAR_FILE = 'target/sample.war'             // WAR file path after build
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build with Maven') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        echo "Deploying ${WAR_FILE} to Tomcat..."
        deploy adapters: [
          tomcat9(credentialsId: 'tomcat-credentials', 
                  path: '', 
                  url: "${TOMCAT_URL}")
        ], 
        contextPath: '/sample', 
        war: "${WAR_FILE}"
      }
    }
  }
}
