pipeline {
    agent any

    tools {
        maven 'Maven3'   // Make sure this name matches Jenkins Global Tool Configuration
    }

    environment {
        IMAGE_NAME = "cicd-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Tag') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    docker tag $IMAGE_NAME $DOCKER_USER/$IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'testin121',
                    passwordVariable: 'Chakri@44'
                )]) {
                    sh 'pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker tag $IMAGE_NAME $DOCKER_USER/$IMAGE_NAME:latest
                    docker push $DOCKER_USER/$IMAGE_NAME:latest
                    docker logout
                    '''
                }
            }
        }
    }
}''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker push $DOCKER_USER/$IMAGE_NAME:latest
                    docker logout
                    '''
                }
            }
        }
    }
}