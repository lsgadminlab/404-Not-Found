pipeline {
    agent any

    environment {
        IMAGE = "docker.lsgserver.dev/not-found:1.0"
    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'registry-auth',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh '''
                    echo $PASS | docker login docker.lsgserver.dev -u $USER --password-stdin
                    docker push $IMAGE
                    '''
                }
            }
        }
    }
}
