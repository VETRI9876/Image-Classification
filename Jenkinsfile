pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'flask-image-classifier'
        DOCKER_TAG = 'latest'
        IMAGE_NAME = 'flask-image-classifier'
        IMAGE_VERSION = 'latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/yourrepository.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t myrepo .'
                }
            }
        }

        stage('Test Docker Image') {
            steps {
                script {
                    // Run Docker container to test
                    sh 'docker run --rm ${DOCKER_IMAGE}:${DOCKER_TAG} python -m unittest discover tests/'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Push Docker image to DockerHub or any other registry
                    sh 'docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} yourdockerhubusername/${DOCKER_IMAGE}:${DOCKER_TAG}'
                    sh 'docker push yourdockerhubusername/${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }

        failure {
            echo 'Build or deployment failed.'
        }
    }
}
