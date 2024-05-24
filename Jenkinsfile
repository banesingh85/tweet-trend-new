pipeline {
    agent any

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64" // Update this path based on your installation
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Verify Java Version') {
            steps {
                sh 'java -version'
            }
        }
        stage('SonarQube analysis') {
            tools {
                sonar 'vproapp-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    sh "${tool 'vproapp-sonar-scanner'}/bin/sonar-scanner"
                }
            }
        }
    }
}
