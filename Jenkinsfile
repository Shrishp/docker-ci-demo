pipeline {
    agent any

    environment {
        // 🧩 Replace with your actual Docker Hub username
        DOCKERHUB_USER = 'shrishp10'
        IMAGE_NAME = 'docker-ci-demo'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '🔄 Checking out source code...'
                git branch: 'main',
                    url: 'https://github.com/Shrishp/docker-ci-demo.git',
                    credentialsId: 'github-cred' // GitHub Personal Access Token (PAT)
            }
        }

        stage('Build App') {
            steps {
                echo '⚙️ Building application...'
                // Example build step (change if your app needs other commands)
                sh 'echo "Building app complete!"'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🐳 Building Docker image...'
                sh '''
                    docker build -t $DOCKERHUB_USER/$IMAGE_NAME:latest .
                '''
            }
        }

        stage('Push to DockerHub') {
            steps {
                echo '📦 Pushing image to DockerHub...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $DOCKERHUB_USER/$IMAGE_NAME:latest
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying application...'
                // Example placeholder (adjust for your environment)
                sh 'echo "Deployment step placeholder"'
            }
        }
    }

    post {
        success {
            echo '✅ Build & Deploy Successful!'
        }
        failure {
            echo '❌ Build Failed'
        }
    }
}
