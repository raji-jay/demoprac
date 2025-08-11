pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "rajijay"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Clone') {
            steps {
                  git branch: 'main', url: 'https://github.com/raji-jay/demoprac.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat """
                docker build -t %DOCKER_IMAGE%:%DOCKER_TAG% .
                """
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                    echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                    docker push %DOCKER_IMAGE%:%DOCKER_TAG%
                    """
                }
            }
        }
    }
}

