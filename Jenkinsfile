pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
                /*For windows machine */
               bat  'mvn clean package'

                /*For Mac & Linux machine */
               // sh  'mvn clean package'
            }

            post{
                success{
                    echo 'Now Archiving ....'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }

        }

        stage ('Deploy Build in Staging Area'){
            steps{

                build job: 'Deploy-StagingArea-Pipeline'
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time: 5, unit: 'Days'){
                    input message: 'Approve PRODUCTION Deployment?',
                }

                build job: 'Deployment-Production-Pipeline'
            }

            post{
                success{
                    echo 'Deployment on PRODUCTION is Successful'
                }

                failure{
                    echo 'Deployment Failure on PRODUCTION'
                }
            }
        }

    }
}
