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
                build job: "deploy-to-staging"
            }
        }

        stage("Deploy to production"){
            steps{
                timeout(time: 5, unit:"DAYS"){
                    input message: "Approve production deployment"
                }

                build job: "deploy-to-production"
            }
            post{
                success{
                    echo "Code deployed to production"
                }

                failure{
                    echo "Deployment failed"
                }
            }
        }
    }
}