pipeline {
    agent any

    environment {
        IMAGE_NAME = 'demoprac'
        IMAGE_TAG = 'latest'
        DOCKER_HUB_USER = 'rajijay'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/raji-jay/demoprac.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Docker Build & Push') {
            steps {
                bat 'docker build -t %DOCKER_HUB_USER%/%IMAGE_NAME%:%IMAGE_TAG% .'

                withCredentials([usernamePassword(credentialsId: 'busapp_credential', usernameVariable: 'DOCKER_HUB_USER', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_HUB_USER% --password-stdin'
                    bat 'docker push %DOCKER_HUB_USER%/%IMAGE_NAME%:%IMAGE_TAG%'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s\\deployment.yaml'
                bat 'kubectl apply -f k8s\\service.yaml'
            }
        }
    }
}


