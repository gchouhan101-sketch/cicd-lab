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
                sh 'docker build -t girjesh111/cicd-app:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push girjesh111/cicd-app:${BUILD_NUMBER}'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f cicd-container || true

                docker run -d \
                --name cicd-container \
                -p 8081:80 \
                girjesh111/cicd-app:${BUILD_NUMBER}
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline Success'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}
