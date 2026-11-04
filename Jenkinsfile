pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                sh 'sudo docker build -t my-java-application:v1 .'
            }
        }
        
        stage('Verify the image') {
            steps {
                sh 'sudo docker images'
            }
        }
    }
}
