pipeline {
    agent any

    environment {
        APP_NAME = "git-testing-app"
        OWNER = "Roshan"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/samtetra/git-testing.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
                echo "Owner: ${OWNER}"
                sh 'python3 app.py'
            }
        }

        stage('Create Artifact') {
            steps {
                sh '''
                mkdir -p output
                echo "Build: ${BUILD_NUMBER}" > output/result.txt
                echo "App: ${APP_NAME}" >> output/result.txt
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'output/*.txt'
        }
    }
}
