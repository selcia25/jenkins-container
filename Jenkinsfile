pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/selcia25/jenkins-container.git', branch: 'main'
            }
        }
        stage('Connect') {
            steps {
                sh '''
                echo "dckr_pat_KYGhDm1IF59UggbfKXddplfTDY8" | docker login -u selcia25 --password-stdin
                '''
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t selcia25/app .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 selcia25/app'
            }
        }
    }
    post {
        always {
            sh 'docker system prune -f'
        }
    }
}
