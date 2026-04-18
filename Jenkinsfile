pipeline {
    agent any
    
    stages {
        stage('Code Checkout') {
            steps {
                git url: 'https://github.com/ArielB1215/test_for_jenkins.git', branch: 'main'
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'export DOCKER_HOST=tcp://host.docker.internal:2375 && docker build -t testforjenkins:0.0.1 .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'export DOCKER_HOST=tcp://host.docker.internal:2375 && docker run -t testforjenkins:0.0.1'
            }
        }
    }
}