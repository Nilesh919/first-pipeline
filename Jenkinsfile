pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git url: 'https://github.com/Nilesh919/first-pipeline.git', branch: 'main'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'echo "Building the app..."'
                // Add actual build/test commands if needed
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                eval $(minikube -p minikube docker-env)
                docker build -t myapp:latest .
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f k8s-deployment.yaml
                kubectl rollout status deployment/myapp -n rudra-app
                '''
            }
        }

    } // End of stages

    post {
        success {
            echo '✅ Pipeline completed successfully! Your app is deployed.'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for errors.'
        }
    }
} // End of pipeline
