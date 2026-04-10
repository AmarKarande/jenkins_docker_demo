pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'hello-world:latest' // Docker Image name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AmarKarande/jenkins_docker_demo.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    if (fileExists('Dockerfile')) {
                        sh "docker build -t ${env.DOCKER_IMAGE} ."
                    } else {
                        error "Dockerfile not found in workspace. Please create one for your application."
                    }
                }
            }
        }

        stage('Docker Run (optional)') {
            steps {
                sh "docker run --rm ${env.DOCKER_IMAGE}"
            }
        }
    }

    post {
        success { echo 'Success' }
        failure { echo 'Failure' }
    }
}
