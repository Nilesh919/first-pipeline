pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "nilesh0824"
        IMAGE_NAME = 'cicd-python-app'
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKERHUB_USER/$IMAGE_NAME:$BUILD_NUMBER .'
            }
        }

        stage('Login to Docker Hub') {
           steps {
              withCredentials([string(credentialsId: 'DOCKERHUB_PASS', variable: 'DOCKERHUB_PASS')]) {
                 sh 'echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin'
            }
          }
       }
        stage('Push Image') {
            steps {
                sh 'docker push $DOCKERHUB_USER/$IMAGE_NAME:$BUILD_NUMBER'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker stop cicd-app || true'
                sh 'docker rm cicd-app || true'
                sh 'docker run -d --name cicd-app -p 5000:5000 $DOCKERHUB_USER/$IMAGE_NAME:$BUILD_NUMBER'
            }
        }
    }
}

