pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                sh 'docker build -t my-java-application:v1 .'
            }
        }
        
        stage('Verify the image') {
            steps {
                sh 'docker images'
            }
        }
    }
}
