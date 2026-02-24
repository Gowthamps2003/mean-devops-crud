pipeline {
    agent any

    environment {
        DOCKER_USER = "gowthamps03"
        FRONTEND_IMAGE = "${DOCKER_USER}/frontend"
        BACKEND_IMAGE  = "${DOCKER_USER}/backend"
        APP_SERVER = "3.109.151.248"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/gowthamps03/mean-devops-crud.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker build -t $FRONTEND_IMAGE:latest ./frontend'
                sh 'docker build -t $BACKEND_IMAGE:latest ./backend'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $FRONTEND_IMAGE:latest'
                sh 'docker push $BACKEND_IMAGE:latest'
            }
        }

        stage('Deploy to EC2') {
            steps {
                withCredentials([sshUserPrivateKey(
                    credentialsId: 'ec2-ssh-key',
                    keyFileVariable: 'SSH_KEY'
                )]) {
                    sh '''
                    ssh -i $SSH_KEY -o StrictHostKeyChecking=no ubuntu@$APP_SERVER "
                        docker pull $FRONTEND_IMAGE:latest &&
                        docker pull $BACKEND_IMAGE:latest &&
                        cd ~/mean-devops-crud &&
                        docker compose down &&
                        docker compose up -d
                    "
                    '''
                }
            }
        }
    }
}
