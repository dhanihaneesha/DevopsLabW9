pipeline{
    agent any
    stages{
        stage('Build Docker Image'){
            steps{
                echo "Build Docker Image..."
                bat "docker build -t kubedemo:v1 ."
            }
        }
        stage('Docker Login'){
            steps{
                bat 'docker login -u dhanihaneesha -p Haneesha@2004'
            }
        }
        stage('push Docker image to Dockerhub'){
            steps{
                echo "push Docker image to Dockerhub..."
                bat "docker tag kubedemoapp:v1 dhanihaneesha/sample:v1"
                bat "docker push dhanihaneesha/sample:kubeimage1"
            }
        }
        stage('Deploy to Kubernetes'){
            steps{
                bat 'kubectl apply -f deployment.yaml --validate'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
}