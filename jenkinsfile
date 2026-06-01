pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checkout Stage Started'
            }
        }

        stage('Build') {
            steps {
                sh 'cat index.html'
            }
        }

        stage('Test') {
            steps {
                echo 'Test Stage Successful'
            }
        }
    }
}
