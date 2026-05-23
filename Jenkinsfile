pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds'       
        IMAGE_REPO = "osama57415/nodejs01"
        IMAGE_TAG  = "${BUILD_NUMBER}" 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/osama275/gitops-by-ci-cd-with-jenkis-and-argocd.git'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    echo 'Logging in to Docker Hub...'
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        echo 'Login successful'
                    }
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    def app = docker.build("${IMAGE_REPO}:${IMAGE_TAG}")
                    
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    echo 'Pushing image to Docker Hub...'
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        def app = docker.image("${IMAGE_REPO}:${IMAGE_TAG}")
                        app.push()
                    }
                }
            }
        }
    }
}

