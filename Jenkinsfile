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
                sh "docker push draganast/api-tests:latest"
                }
        }
    }
}
