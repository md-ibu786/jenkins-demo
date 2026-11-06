pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'ibrahim2903/my-java-app'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout Source Code from SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$IMAGE_TAG .'
            }
        }
        
        stage('Verify the image') {
            steps {
                sh 'docker images'
            }
        }
        
        stage('Push to DockerHub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub_cred',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                        -u "$DOCKER_USER" --password-stdin

                        docker push "$DOCKER_IMAGE:$IMAGE_TAG"

                        docker logout
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo "Image Pushed success"
        }
        
        failure {
            echo "Pipeline failed"
        }
    }
}
