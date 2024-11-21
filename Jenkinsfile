pipeline {
    agent any
   
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/selcia25/jenkins-container.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t selcia25/flaskapp .'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Optionally, push the Docker image to DockerHub or another registry
                    // sh 'docker push $DOCKER_REGISTRY/$DOCKER_IMAGE:$DOCKER_TAG'

                    // Optionally, deploy the container to a server or cloud
                    sh 'docker run -p 5000:5000 selcia25/flaskapp'
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
