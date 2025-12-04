pipeline {
  agent any

  tools {
    maven 'Maven'
    jdk 'Java17'
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
        sh 'mvn test || true'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

    stage('Deploy to Test Server') {
      steps {
        sshagent(['d591e1a7-05b7-404a-ad99-8b295b95cb46']) {  // Your Jenkins Credential ID
          sh '''
            echo "Copying WAR to Test Server..."
            scp target/*.war manisha@172.19.182.35:/tmp/MyApp.war

            echo "Deploying WAR to Tomcat..."
            ssh manisha@172.19.182.35 "
              sudo mv /tmp/MyApp.war /var/lib/tomcat9/webapps/MyApp.war &&
              sudo systemctl restart tomcat9
            "
          '''
        }
      }
    }

  } // end stages
} // end pipeline

