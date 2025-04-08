pipeline {
    agent any
    stages{
        stage('checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Parth2k3/test-django'
            }
        }
        stage('Login to ECR'){
            steps{
                withAWS(region: 'ap-south-1', credentials: 'aws-creds'){
                    powershell '''
                    $password = aws ecr get-login-password --region ap-south-1
                    docker login --username AWS --password $password 864981751441.dkr.ecr.ap-south-1.amazonaws.com
                    '''
                }
            }
        }
        stage('Build docker image'){
            steps{
                powershell '''
                docker build -t test:django .
                docker tag test:django 864981751441.dkr.ecr.ap-south-1.amazonaws.com/test:django
                '''
            }
        }
        stage('Pushing image to ECR'){
            steps{
                powershell '''
                docker push 864981751441.dkr.ecr.ap-south-1.amazonaws.com/test:django
                '''
            }
        }
    }
}
