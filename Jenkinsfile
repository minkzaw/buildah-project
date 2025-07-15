pipeline {
    agent any

    stages {
        stage ('Print Hello') {
            steps {
                echo "Hello World!"
            }
        }
        
        stage('Build Image with Buildah') {
            steps {
                container('buildah') {
                    sh 'buildah bud -t my-nginx .'
                }
            }
        }

        stage('List Local Images (Optional)') {
            steps {
                container('buildah') {
                    sh 'buildah images'
                }
            }
        }
    }
}
