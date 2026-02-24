pipeline {
    agent any

    environment {
        DOCKER_USER = "yourdockerhubusername"
        FRONTEND_IMAGE = "yourdockerhubusername/frontend"
        BACKEND_IMAGE = "yourdockerhubusername/backend"
        APP_SERVER = "3.109.151.248"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Gowthamps2003/mean-devops-crud.git'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker build -t $FRONTEND_IMAGE:latest ./frontend'
                sh 'docker build -t $BACKEND_IMAGE:latest ./backend'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $FRONTEND_IMAGE:latest'
                sh 'docker push $BACKEND_IMAGE:latest'
            }
        }

        stage('Deploy to App EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no ubuntu@$3.109.151.248 '
                    docker pull $FRONTEND_IMAGE:latest &&
                    docker pull $BACKEND_IMAGE:latest &&
                    docker-compose down &&
                    docker-compose up -d
                    '
                    """
                }
            }
        }
    }
}
