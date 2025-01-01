pipeline {
    agent any
    environment {
        // Define Docker image names with your Docker Hub username
        DOCKER_IMAGE_BACKEND = "livhere/chat-app-backend"
        DOCKER_IMAGE_FRONTEND = "livhere/chat-app-frontend"
    }
    stages {
        stage('Build Backend') {
            steps {
                script {
                    // Build Docker image for the backend
                    sh 'docker build -t $DOCKER_IMAGE_BACKEND -f backend/Dockerfile .'
                }
            }
        }
        stage('Build Frontend') {
            steps {
                script {
                    // Build Docker image for the frontend
                    sh 'docker build -t $DOCKER_IMAGE_FRONTEND -f frontend/Dockerfile .'
                }
            }
        }
        stage('Docker Login and Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                                                     usernameVariable: 'DOCKER_USERNAME', 
                                                     passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Login to Docker Hub
                        sh '''
                            echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        '''

                        // Push Docker images to Docker Hub
                        sh 'docker push $DOCKER_IMAGE_BACKEND'
                        sh 'docker push $DOCKER_IMAGE_FRONTEND'

                        // Logout from Docker Hub
                        sh 'docker logout'
                    }
                }
            }
        }
    }
    post {
        always {
            // Clean up containers and images after the pipeline runs
            sh '''
                docker ps -q | xargs -r docker stop
                docker ps -a -q | xargs -r docker rm
                docker images -q | xargs -r docker rmi -f
            '''
        }
    }
}
