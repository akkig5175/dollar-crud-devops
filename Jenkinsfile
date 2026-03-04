pipeline {
    agent any

    environment {
        DOCKER_USER = "akki5175"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/akkig5175/dollar-crud-devops.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh "docker build -t $DOCKER_USER/dollar-backend:$IMAGE_TAG ./backend"
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh "docker build -t $DOCKER_USER/dollar-frontend:$IMAGE_TAG ./frontend"
            }
        }

        stage('Push Images to DockerHub') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'dockerhub_cred', usernameVariable: 'USER', passwordVariable: 'PASS')
                ]) {
                    sh """
                        echo \$PASS | docker login -u \$USER --password-stdin
                        docker push $DOCKER_USER/dollar-backend:$IMAGE_TAG
                        docker push $DOCKER_USER/dollar-frontend:$IMAGE_TAG
                    """
                }
            }
        }

        stage('Deploy to Hosting VM') {
            steps {
                withCredentials([
                    string(credentialsId: 'HOST_IP', variable: 'HOST'),
                    sshUserPrivateKey(credentialsId: 'server-ssh', keyFileVariable: 'SSH_KEY')
                ]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no -i \$SSH_KEY ubuntu@\$HOST '
                            cd mean-app &&
                            export IMAGE_TAG=$IMAGE_TAG &&
                            docker-compose pull &&
                            docker-compose up -d
                        '
                    """
                }
            }
        }
    }
}
