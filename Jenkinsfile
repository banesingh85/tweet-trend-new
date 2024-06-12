pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment {
         PATH = "/opt/apache-maven-3.9.6/bin:$PATH" 
         DOCKER_CREDENTIALS_ID = 'dockerhub_cred'
         DOCKER_IMAGE = 'banesingh85/ttrend'
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('build docker image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }
        stage('push docker image on dockerhub') {
           steps {
            script {
                docker.image("${DOCKER_IMAGE}:${env.BUILD_ID}").push()
                docker.image("${DOCKER_IMAGE}:${env.BUILD_ID}").push('latest')
    }
}
}
 }
}