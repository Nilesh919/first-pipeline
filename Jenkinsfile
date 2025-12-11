pipeline {
    agent any

    stages {

        // Step 1: Clone code from GitHub (CI)
        stage('Clone Code') {
            steps {
                git url: 'https://github.com/Nilesh919/first-pipeline.git', branch: 'main'
            }
        }

        // Step 2: Build / Test the project (CI)
        stage('Build & Test') {
            steps {
                sh 'echo "Building the app..."'
                // Add actual build/test commands if you have any
            }
        }

        // Step 3: Docker Build (CD)
        stage('Docker Build') {
            steps {
                sh '''
                # Use Minikube's Docker daemon
                eval $(minikube -p minikube docker-env)

                # Build Docker image
                docker build -t myapp:latest .
                '''
            }
        }

        // Step 4: Deploy to Kubernetes (CD)
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                # Apply Kubernetes deployment YAML
                kubectl apply -f k8s-deployment.yaml

                # Wait for rollout to complete
                kubectl rollout status deployment/myapp -n rudra-app
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully! Your app is deployed.'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for errors.'
        }
    }
}

            }
        }
    }
}

