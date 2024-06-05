pipeline {
    agent any
    environment {
        SONARQUBE_SCANNER_PARAMS = '{"sonar.organization":"vproapp01", "sonar.projectKey":"vproapp01-key_ttrend-vpro", "sonar.host.url":"https://sonarcloud.io"}'
    }
    stages {
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    sh 'sonar-scanner -X -Dsonar.organization=vproapp01 -Dsonar.projectKey=vproapp01-key_ttrend-vpro -Dsonar.host.url=https://sonarcloud.io'
                }
            }
        }
    }
}
