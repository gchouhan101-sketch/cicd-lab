pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'cat index.html'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t cicd-app:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f cicd-container || true

                docker run -d \
                --name cicd-container \
                -p 8081:80 \
                cicd-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}
