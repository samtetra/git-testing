pipeline {
    agent any

    environment {
        APP_NAME = "git-testing-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        DOCKERHUB_USER = "mohamadalii"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/samtetra/git-testing.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKERHUB_USER/$APP_NAME:$IMAGE_TAG .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKERHUB_USER/$APP_NAME:$IMAGE_TAG'
            }
        }
    }
}
