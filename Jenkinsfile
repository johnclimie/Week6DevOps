pipeline{
    agent any
    stages{
        stage('Checkout Code'){
            steps{
                git branch: 'main', url: 'https://github.com/johnclimie/Week6DevOps'
            }
        }
        stage('Build'){
            steps{
                sh 'echo "building the app"'
            }
        }
        stage('Test'){
            steps{
                sh 'echo "Running tests"'
            }
        }
        stage('Deploy'){
            steps{
                sh 'echo "deploying"'
            }
        }
    }
}
