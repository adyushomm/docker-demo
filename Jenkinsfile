pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Pulls the latest code from your GitHub repository
                git branch: 'main', url: 'https://github.com/adyushomm/docker-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Builds the docker image from your Dockerfile
                sh 'docker build -t dockerdemo:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                // Removes old container if running to prevent port conflicts
                sh 'docker stop my-app || true'
                sh 'docker rm my-app || true'
            }
        }

        stage('Deploy Container') {
            steps {
                // Runs the newly built image on port 5000 mapped to container port 80
                sh 'docker run -d -p 5000:80 --name my-app dockerdemo:latest'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Application is live on port 5000.'
        }
        failure {
            echo 'Pipeline failed. Check build logs for errors.'
        }
    }
}
