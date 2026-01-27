pipeline {
  agent any
  tools {
        maven 'maven3' // El nombre que le diste en la configuración
        dockerTool 'docker'
    }
  environment {
    IMAGE_NAME = "demo-ci-cd:latest"
  }
  stages {
    stage('Checkout') {
      steps {
        //checkout scm
        git branch: 'main', url: 'https://github.com/herbert-code/springboot-app.git'
      }
    }
    stage('Build & Test') {
      steps {
        sh 'mvn -B clean package'
        //echo 'Maven Comands Step'
      }
    }
    stage('Run Application with Java') {
      steps {
        sh 'java -jar target/demo-0.0.1-SNAPSHOT.jar --server.port=9090 &'
        sh 'sleep 10'        
      }
    }
    stage('App Verification') {
      steps {                
        sh 'curl http://localhost:9090'
        sh 'sleep 20'
        echo 'Aplicación funcionando'
      }
    }
    
    stage('Run Application with Maven') {
      steps {
        //sh 'mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=9090 &'
        //sh 'sleep 30'
        echo 'Run with Maven'
      }
    }
    stage('Build Docker Image') {
      steps {
        //sh 'docker build -t $IMAGE_NAME .'
        echo 'Docker Build Image Step'
      }
    }
    stage('Run Container') {
      steps {
        //sh 'docker rm -f demo-ci-cd || true'
        //sh 'docker run -d --name demo-ci-cd -p 8080:8080 $IMAGE_NAME'
        echo 'Docker Run Container Step'
      }
    }
  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    }
  }
}