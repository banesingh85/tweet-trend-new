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
                docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                docker.image("${DOCKER_IMAGE}:${env.BUILD_ID}").push()
                docker.image("${DOCKER_IMAGE}:${env.BUILD_ID}").push('latest')
            }
          }
        }
       }
       stage('Clean Up Old Docker Images') {
            steps {
                script {
                    try {
                        def images = sh(script: "docker images --format '{{.Repository}}:{{.Tag}} {{.CreatedAt}}' | grep '${DOCKER_IMAGE}' | sort -r | tail -n +${KEEP_LATEST_N + 1}", returnStdout: true).trim()
                        if (images) {
                            images.split('\n').each { image ->
                                def imageId = image.split(' ')[0]
                                sh "docker rmi ${imageId} || true"
                            }
                        }
                    } catch (Exception e) {
                        error "Failed to clean up old Docker images: ${e.message}"
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
