pipeline{
    agent any
    environment{
        IMAGE_NAME = 'parth2k3/test-django'
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Parth2k3/test-django'
            }
        }
        stage('Build docker image'){
            steps{
                powershell '''
                docker build -t ${IMAGE_NAME}:latest .
                '''
            }
        }
        stage('Push to dockerhub'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
                    powershell '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push ${IMAGE_NAME}:latest
                    docker logout
                    '''
                }
            }
        }
    }
}
