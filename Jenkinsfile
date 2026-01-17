pipeline {
    agent any

    environment {
        AWS_REGION = 'us-west-1'
        AWS_ACCOUNT_ID = '008585377828'
        IMAGE_NAME = 'meetingbot-example-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
            url: 'https://github.com/himanshi1107/meetingbot-app.git'
            }
        }
        
        stage('Build Docker Image'){
            steps{
                sh '''
                    docker build -t ${IMAGE_NAME}:latest src/example-app
                '''
            }
        }
        
        stage('Login to Amazon ECR'){
            steps{
                sh '''
                    aws ecr get-login-password --region ${AWS_REGION} \
                    | docker login --username AWS \
                    --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com
                '''
            }
        }
        
        stage('Tag Docker Image'){
            steps{
                sh '''
                    docker tag ${IMAGE_NAME}:latest \
                    ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${IMAGE_NAME}:latest
                '''
            }
        }
        stage('Push Image to ECR'){
            steps{
                sh '''
                    docker push \
                    ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${IMAGE_NAME}:latest
                '''
            }
        }
    }
}
