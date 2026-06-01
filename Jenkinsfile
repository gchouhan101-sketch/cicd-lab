

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

        stage('Docker Images') {
            steps {
                sh 'docker images | grep cicd-app'
            }
        }
    }

    post {
        success {
            echo 'Docker Build Success'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}
