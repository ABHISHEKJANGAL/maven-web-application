pipeline
{
    agent any

    tools
    {
        maven 'Maven_3.9.9'
    }

    environment
    {
        buildNumber = "${BUILD_NUMBER}"
    }

    stages
    {
        stage('Checkout Code to Jenkins from GitHub')
        {
            steps()
            {
                git branch: 'DevOpsJulyBatch', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
            }
        }

        stage('Build Artifact using Maven')
        {
            steps()
            {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image')
        {
            steps()
            {
                sh 'docker build -t 149536451818.dkr.ecr.ap-south-1.amazonaws.com/login-application:${buildNumber} .'
            }
        }

        stage('Authenticate and Push Docker Image to AWS ECR')
        {
            steps()
            {
                sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 149536451818.dkr.ecr.ap-south-1.amazonaws.com'
                sh 'docker push 149536451818.dkr.ecr.ap-south-1.amazonaws.com/login-application:${buildNumber}'
            }
        }

        stage('Remove Docker Image from Jenkins Locally')
        {
            steps()
            {
                sh 'docker rmi -f 149536451818.dkr.ecr.ap-south-1.amazonaws.com/login-application:${buildNumber}'
            }
        }

        stage('Update Image Tag in Kubernetes Manifest')
        {
            steps()
            {
                sh "sed -i 's/Build_Tag/${buildNumber}/g' MavenWebApplication.yaml"
            }
        }

        #Deployment stage
        stage('Deploy Application in AWS EKS Cluster')
        {
            steps()
            {
                sh 'kubectl delete deployment webpage-deployment -n production || true'
                sh 'kubectl apply -f MavenWebApplication.yaml'
            }
        }
    }
}