pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-nginx'
    }

    stages {
        
        stage('Build Image with Buildah') {
            steps {
                script {
                    sh 'buildah bud -t $IMAGE_NAME .'
                }
            }
        }

        stage('List Local Images (Optional)') {
            steps {
                sh 'buildah images'
            }
        }
    }
}
