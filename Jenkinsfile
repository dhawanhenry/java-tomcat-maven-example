pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
                bat 'mvn clean package'
            }

            post {
                success {
                    echo 'Now Archiving ....'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }

        stage ('Deploy Build in Staging Area'){
            steps{
                build job : 'Deploy-StagingArea-Pipeline'
            }
        }

        stage ('Deploy To Prod'){
            steps{
                timeout (time: 5, unit: 'DAYS'){
                    input message : 'Approve Production Deployment?'
            }
                build job : 'Deploy-Production-Pipeline'
            }

            post{
                success{
                    echo 'Deployment on Production is Successful'
                }

                failure{
                    echo 'Deployment Failure on Production'
                }
            }
        }
    }
}
