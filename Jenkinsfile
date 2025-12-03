pipeline {
  agent any

  tools {
    maven 'Maven'     // The Maven installation you configured in Jenkins
    jdk 'Java17'      // The JDK you configured in Jenkins
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/DEV8428/MyJavaApp.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean compile'
      }
    }
    stage('Test') {
      steps {
        // if you have tests in future; for now just compile
        sh 'mvn test || true'
      }
    }
    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }
    // You can add more stages later: e.g. deploy
  }
}

