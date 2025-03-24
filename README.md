# StudentProject - Multi-App Django Deployment with Docker & Jenkins

## Overview
StudentProject is a Django-based web application containing multiple apps, designed to be containerized using Docker and deployed via Jenkins CI/CD pipeline. This project demonstrates a simple static content website without a database.

## Features
- Multi-app Django project
- Static views and templates
- Containerized using Docker
- Automated deployment using Jenkins
- Hosted Docker image on Docker Hub

## Project Structure
```
StudentProject/
│── app1/
│   ├── templates/app1/
│   │   ├── index.html
│   │   ├── sample.html
│   ├── views.py
│── app2/
│   ├── templates/app2/
│   │   ├── sample.html
│   ├── views.py
│── templates/
│   ├── base.html
│── Dockerfile
│── Jenkinsfile
│── requirements.txt
│── manage.py
│── README.md
```

## Installation & Setup
### Prerequisites
- Docker installed
- Python 3.x installed
- Jenkins setup (optional for CI/CD)

### Running Locally
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/StudentProject.git
   cd StudentProject
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```
3. Run the Django server:
   ```sh
   python manage.py runserver
   ```
4. Open `http://127.0.0.1:8000/` in your browser.

## Dockerization
### Build and Run Docker Container
1. Build the Docker image:
   ```sh
   docker build -t yashr22/studentproject .
   ```
2. Run the container:
   ```sh
   docker run -p 8000:8000 yashr22/studentproject
   ```

### Docker Hub Deployment
1. Login to Docker Hub:
   ```sh
   docker login
   ```
2. Push the image:
   ```sh
   docker push yashr22/studentproject
   ```

## Jenkins CI/CD Pipeline
### Jenkinsfile Steps:
1. Clone repository from GitHub
2. Build Docker image
3. Push image to Docker Hub

### Sample Jenkinsfile:
```groovy
pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/StudentProject.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t yashr22/studentproject .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push yashr22/studentproject'
                }
            }
        }
    }
}
```

