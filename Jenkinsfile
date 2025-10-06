pipeline{
    agent any
    stages{
        stage('Build Docker Image'){
            steps{
                echo "Build Docker Image..."
                bat "docker build -t kubedemo:v1 ."
            }
        }
        steps {
    withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
        bat '''
            docker login -u %DOCKER_USER% -p %DOCKER_PASS%
        '''
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
