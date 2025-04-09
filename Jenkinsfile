pipeline {
    agent any

    environment {
        VENV = 'venv'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch:'main', url:'https://github.com/Parth2k3/test-django.git'
            }
        }

        stage('Set up Python Virtual Env') {
            steps {
                bat 'python -m venv %VENV%'
                bat '%VENV%\\Scripts\\python -m pip install --upgrade pip'
                bat '%VENV%\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run Django Tests') {
            steps {
                bat '%VENV%\\Scripts\\python manage.py test'
            }
        }
    }
}
