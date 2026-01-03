pipeline
{
    agent any

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
    }
}