pipeline {
    agent any
    stages {
        stage('ECR login') {
            steps {
                sh "aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ECR_REPO}"
            }
        }
        stage('Build & Push') {
            steps {
                sh "docker info"
                sh "docker buildx build --platform ${PLATFORMS} -t ${ECR_REPO}/${ECR_REPO_NAME}:${BUILD_NUMBER} . --push"
            }
        }
    }
}

