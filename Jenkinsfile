pipeline {
    agent any

    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/banesingh85/tweet-trend-new.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean deploy -X'
                archiveArtifacts 'target/surefire-reports/*.xml'
            }
        }

        stage('SonarQube analysis') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            environment {
                scannerHome = tool 'vproapp-sonar-scanner'
                JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
                PATH = "${JAVA_HOME}/bin:${env.PATH}"
            }
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    sh 'java -version' // Verify the Java version
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
