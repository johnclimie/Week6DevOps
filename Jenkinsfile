pipeline{
    agent any
    environment {
        IMAGE_NAME = 'johnclimie/Week6DevOps'
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/johnclimie/Week6DevOps'
            }
        }
        stage('Build Docker image'){
            steps{
                sh "docker build -t %IMAGE_NAME%:latest ."
            }
        }
        stage('Push to Dockerhub'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
                    sh """
                    echo %DOCKER_PASS% | 
                    docker login -u %DOCKER_USER% -- password-stdin
                    docker push %IMAGE_NAME%:latest
                    docker logout
                    """
                }
            }
        }
    }
}
