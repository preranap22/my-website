pipeline {
    agent any

    environment {
        DOCKER_USER_NAME = "ptl2209"

        DOCKER_IMAGE_NAME = "my-website"

    }

    stages {
        stage('SCM') {
            steps {
            git 'https://github.com/preranap22/my-website.git'
            }
        }

        stage('build docker image'){
            steps {
            sh 'docker image build -t ${DOCKER_USER_NAME}/${DOCKER_IMAGE_NAME} .'
            }
        }

        stage('docker login'){
            steps{
            withCredentials([string(credentialsId: 'DOCKER_ACCESS_TOKEN', variable: 'DOCKER_HUB_ACCESS_TOKEN')]) {
                sh 'echo ${DOCKER_HUB_ACCESS_TOKEN} | docker login -u ${DOCKER_USER_NAME} --password-stdin'    
            }
            }
        }

        stage('push docker image'){
            steps {
            sh 'docker image push ${DOCKER_USER_NAME}/${DOCKER_IMAGE_NAME}'
            }
        }

        stage('minikube start'){
            steps{
                sh 'minikube start'
            }

        }

        stage('create pod'){
            steps {
                sh 'kubectl create -f pod1.yaml'
            }
        }
    }
}
