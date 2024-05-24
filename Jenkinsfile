pipeline {
    agent {
        node {
        label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
}

    stages {
        stage('build') {
            steps {
                sh 'mvn clean deploy' 
            }
          }
    stage('SonarQube analysis') {
     environment {
                scannerHome = tool 'vproapp-sonar-scanner'
                JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64" // Update this path based on your installation
                PATH = "${JAVA_HOME}/bin:${env.PATH}"
            }

    steps{
    withSonarQubeEnv('sonarqube-server') { // ##If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }       
}
}
