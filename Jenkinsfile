pipeline {
  agent any

  tools {
    maven 'Maven'
    jdk 'Java17'
  }

  environment {
    MAVEN_OPTS = '-Dmaven.repo.local=/path/to/your/cache/.m2'  // Optional for caching
  }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/DEV8428/MyJavaApp.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('Test') {
      steps {
        catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
          sh 'mvn test'
        }
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

  } // end stages
  
  post {
    always {
      cleanWs()  // Clean up workspace after the build
    }
  }

} // end pipeline
