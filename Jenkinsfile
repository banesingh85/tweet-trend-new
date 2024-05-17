pipeline {
    agent {
        node {
        label 'maven'
        }
    }

    stages {
        stage('Clone-Code') {
            steps {
                git branch: 'main', url: 'https://github.com/banesingh85/tweet-trend-new.git'
            }
        }
    }
}
