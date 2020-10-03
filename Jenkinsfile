pipeline{
    agent { label "master" }
    environment {
        ECR_REGISTRY = "094879549578.dkr.ecr.us-east-1.amazonaws.com"
        APP_REPO_NAME = "zey-repo/phonebook-app"
        AWS_REGION = "us-east-1"
    }
    stages {
        stage('Create ECR Repo') {
            steps {
            echo 'Creating ECR Repository'
            sh """
            aws ecr create-repository \
              --repository-name ${APP_REPO_NAME} \
              --imaage-scanning-configuration scanOnPush=false \
              --image-tag-mutability MUTABLE \
              --region ${AWS_REGION}
            """
            }
        }
        stage('Build App Docker Images'){
            steps {
                echo 'Building app Docker images'
            }
        }
        stage('Push Docker Images to ECR Repo'){
            steps {
                echo 'Pushing images to ECR'
            }
        }
        stage('Create Infrastructure for the App'){
            steps {
                echo 'Creating Docker Swarm'
            }
        }
        stage('Test the Infrastructure'){
            steps {
                echo 'Testing if Docker Swarm is ready or not'
            }
        }
        stage('Deploy the App on Docker Swarm'){
            steps {
                echo 'Deploying the app'
            }
        }
        stage('Test the application'){
            steps {
                echo 'Check if the application is ready or not'
            }
        }
    }
    post {
        always {
            echo 'Deleting all local images'
        }
        failure {
            echo 'Deleting the image repository on ECR due to failure'
            echo 'Deleting the cloudformation stack due to failure'
        }
    }
}