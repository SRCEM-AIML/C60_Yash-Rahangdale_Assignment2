pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPO_NAME.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t YOUR_DOCKER_HUB_USERNAME/studentproject .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                        sh 'docker push YOUR_DOCKER_HUB_USERNAME/studentproject'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d -p 8000:8000 YOUR_DOCKER_HUB_USERNAME/studentproject'
                }
            }
        }
    }
}
