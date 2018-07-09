pipeline {
    agent any
   
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage("deploy to stage"){
            steps{
                build job: "Deploy-to-staging"
            }
        }
    }
}