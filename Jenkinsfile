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
        
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    sh './health-check.sh'
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}