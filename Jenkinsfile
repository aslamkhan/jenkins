pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                git 'https://github.com/aslamkhan/jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    dockerImage = docker.build('nasb-demo')
                }
            }
        }

        stage('Run Docker Container Locally') {
            steps {
                // Run Docker container locally
                script {
                    dockerImage.run('-p 3000:3000 --name nasb-demo-container -d')
                }
            }
        }

        stage('Cleanup') {
            steps {
                // Clean up resources
                script {
                    dockerImage.stop()
                    dockerImage.remove()
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
