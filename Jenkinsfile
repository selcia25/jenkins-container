pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'flaskapp'
        DOCKER_REGISTRY = 'selcia25'
        DOCKER_TAG = 'latest'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/selcia25/jenkins-container.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_REGISTRY/$DOCKER_IMAGE:$DOCKER_TAG .'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Optionally, push the Docker image to DockerHub or another registry
                    // sh 'docker push $DOCKER_REGISTRY/$DOCKER_IMAGE:$DOCKER_TAG'

                    // Optionally, deploy the container to a server or cloud
                    sh 'docker run -d -p 5000:5000 $DOCKER_REGISTRY/$DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }
    }
    post {
        always {
            // Cleanup any resources or containers
            sh 'docker system prune -f'
        }
    }
}
