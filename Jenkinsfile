pipeline {
    agent any
    stages {
        stage ('Initializing the Code File') {
            steps {
                sh '''
                echo "PATH = ${PATH}"
                echo "M2_HOME = ${M2_HOME}"
                '''
            }

        }

        stage ('Build'){
            steps{
                echo 'Hello World everyone.'
            }
        }
    }
}
