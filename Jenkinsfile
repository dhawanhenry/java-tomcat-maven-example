pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
                bat 'mnv clean package'
            }

            post {
                success {
                    echo 'Now Archiving ....'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }

        stage ('Develop Build Staging Area'){
            steps{
                build job : 'Develop-StagingArea-Pipeline'
            }
        }
    }
}
