pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'node-app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t ${DOCKER_IMAGE_NAME} .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    sh 'docker run -d --name ${DOCKER_IMAGE_NAME}-container ${DOCKER_IMAGE_NAME}'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run tests inside the running Docker container
                    sh 'docker exec ${DOCKER_IMAGE_NAME}-container npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Placeholder for deployment steps
                    echo "Deploying application..."
                    // Example: push Docker image to registry or deploy the container
                    // sh 'docker push ${DOCKER_IMAGE_NAME}' (if using a Docker registry)
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Stop and remove the Docker container and image
                    sh 'docker stop ${DOCKER_IMAGE_NAME}-container'
                    sh 'docker rm ${DOCKER_IMAGE_NAME}-container'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images and containers after the pipeline
            sh 'docker rmi ${DOCKER_IMAGE_NAME}'
        }
        success {
            // Notify on success (can be enhanced with real notifications)
            echo "Build, test, and deployment succeeded!"
        }
        failure {
            // Notify on failure (can be enhanced with real notifications)
            echo "Build, test, or deployment failed!"
        }
    }
}

