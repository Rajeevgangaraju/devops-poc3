pipeline {
    agent any

    environment {
        IMAGE = "my-devops-app"
        CONTAINER = "my-devops-container"
    }

    stages {
        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop $CONTAINER || true
                docker rm $CONTAINER || true
                docker run -d -p 81:80 --name $CONTAINER $IMAGE
                '''
            }
        }
    }
}
