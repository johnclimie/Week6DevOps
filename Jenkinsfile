tpipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-2'
        IMAGE_NAME = 'dev-test'
        IMAGE_TAG = 'latest'
        REPO_NAME = 'test'
        AWS_ACCOUNT_ID = '451947743265'
        ECR_URL = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/johnclimie/Week6DevOps'
            }
        }

        stage('Login to ECR') {
            steps {
                withAWS(region: "${env.AWS_REGION}", credentials: 'aws-creds') {
                    powershell '''
                        aws ecr get-login-password --region $env:AWS_REGION | docker login --username AWS --password-stdin $env:ECR_URL
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                powershell '''
                    docker build -t "$env:IMAGE_NAME:$env:IMAGE_TAG" .
                    docker tag "$env:IMAGE_NAME:$env:IMAGE_TAG" "$env:ECR_URL/$env:REPO_NAME:$env:IMAGE_TAG"
                '''
            }
        }

        stage('Push to ECR') {
            steps {
                powershell '''
                    docker push "$env:ECR_URL/$env:REPO_NAME:$env:IMAGE_TAG"
                '''
            }
        }
    }
}
