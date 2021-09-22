pipeline {
    agent any
    stages {
        stage('ECR login & tag delete') {
            steps {
                sh "aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ECR_REPO}"
                sh "aws ecr batch-delete-image --repository-name ${ECR_REPO_NAME} --image-ids imageTag=latest"
            }
        }
        stage('Build & Push') {
            steps {
                sh "docker info"
                sh "docker buildx build --platform ${PLATFORMS} -t ${ECR_REPO}/${ECR_REPO_NAME}:${BUILD_NUMBER} -t ${ECR_REPO}/${ECR_REPO_NAME}:latest . --push"
            }
        }
    }
}

