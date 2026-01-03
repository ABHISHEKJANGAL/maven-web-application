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
    }
}