pipeline {
    agent any
    triggers {
        pollSCM('*/1 * * * *')
    }
    stages {
        stage('get-code') {
            steps {
                echo "Obtaining code from GitHub repository"
                git branch: "main", url: "https://github.com/dragana-st/api-tests-final.git"
            }
        }

        stage('build-docker-image') {
            steps {
                echo "Building docker image from Dockerfile"
                sh "docker build -t draganast/api-tests:latest ."
            }
        }

        stage('push-docker-image') {
            steps {
                echo "Pushing docker image to Docker Hub"
                withCredentials([usernamePassword(
                    credentialsId: 'DockerHub-Credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push draganast/api-tests:latest
                    """
                }
            }
        }
    }
}
