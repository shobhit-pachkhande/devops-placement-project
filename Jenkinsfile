pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "shobhitpach/user-service"   // ✅ Correct image name
        DOCKERHUB_CREDENTIALS = 'dockerhub'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/shobhit-pachkhande/devops-placement-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('user-service') { // ✅ Go to the correct subdirectory
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "$DOCKERHUB_CREDENTIALS", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }
}
