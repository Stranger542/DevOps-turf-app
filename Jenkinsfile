pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'sumit2023bcd0026' 
        REG_NUMBER = '2023bcd0026'
        ROLL_NUMBER = '26'
        IMAGE_NAME = "${DOCKER_HUB_USER}/${REG_NUMBER}_${ROLL_NUMBER}"
        DOCKER_CREDS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout Code') { 
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker Image: ${IMAGE_NAME}"
                    // Builds the image locally
                    sh "docker build -t ${IMAGE_NAME} ." 
                }
            }
        }
        
        stage('Push to Docker Hub') { 
            steps {
                script {
                    sh "echo ${DOCKER_CREDS_PSW} | docker login -u ${DOCKER_CREDS_USR} --password-stdin"
                    echo "Pushing Image to Docker Hub..."
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }
    }
    
    post {
        always {
            sh "docker rmi ${IMAGE_NAME} || true"
            sh "docker logout"
        }
    }
}
