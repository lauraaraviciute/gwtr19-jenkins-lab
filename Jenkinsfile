pipeline {
    agent { docker { image 'python:3.5.1' } }
 
    environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
    }
    stages {
        stage('Credentials Stage') {
            steps {
                echo 'Using the Credentials Plugin'
                withCredentials([string(credentialsId: 'jenkins-aws-secret-key-id', variable: 'PW1')]) {
                        echo "My password is '${PW1}'!"
                }
 
                echo 'using credentials method'
                sh 'echo aws-secret-key-id=$AWS_ACCESS_KEY_ID'
                sh 'echo aws-secret-access-key=$AWS_SECRET_ACCESS_KEY'
            }
        }
    }
}