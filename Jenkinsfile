pipeline {
    agent any

    environment {
        AWS_REGION = 'us-west-1'
        AWS_ACCOUNT_ID = '008585377828'
        EXAMPLE_APP_IMAGE = 'meetingbot-example-app'
        SERVER_IMAGE = 'meetingbot-server'
        APP_VERSION = 'v1.0.1'
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
                    docker build -t ${EXAMPLE_APP_IMAGE}:latest src/example-app
                '''
            }
        }
        
        stage('Build Server Docker Image') {
            steps {
                sh '''
                    docker build -t ${SERVER_IMAGE}:latest src/server
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
        
        stage('Tag Docker Images'){
            steps{
                sh '''
                    docker tag ${EXAMPLE_APP_IMAGE}:latest \
                    ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${EXAMPLE_APP_IMAGE}:${APP_VERSION}

                    docker tag ${SERVER_IMAGE}:latest \
                    ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${SERVER_IMAGE}:latest
                '''
            }
        }
        stage('Push Image to ECR'){
            steps{
                sh '''
                    docker push \
                    ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${EXAMPLE_APP_IMAGE}:${APP_VERSION}

                    docker push \
                    ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${SERVER_IMAGE}:latest
                '''
            }
        }
        
        stage('Deploy Example App to ECS') {
            steps {
                sh '''
                    aws ecs update-service \
                      --cluster meetingbot-ec2-jenkins-cluster \
                      --service meetingbot-example-app-task-service-s85efvrn \
                      --force-new-deployment \
                      --region ${AWS_REGION}
                '''
            }
}

    }
}
