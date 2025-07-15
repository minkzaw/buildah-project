pipeline {
    agent any
    environment {
        REGISTRY = 'quay.io'
        IMAGE_NAME = 'mkzaw/buildah-project'
        CACHE_DIR = 'mkzaw/buildah-project/cache'
        TAG = "${BUILD_NUMBER}"
    }
    stages {
        stage ('Hello from Jenkins') {
            steps {
                sh 'echo "Hello World"'
            }
        }
        stage ('Build with buildah') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'buildah-project',
                    usernameVariable: 'REGISTRY_USER',
                    passwordVariable: 'REGISTRY_PASS'
                )]) {
                    container ('buildah') {
                        sh 'buildah login -u $REGISTRY_USER -p $REGISTRY_PASS quay.io'
                    }
                }
            }
            steps {
                container('buildah') {
                    sh 'buildah bud --layers --cache-from $REGISTRY/$CACHE_DIR --cache-to $REGISTRY/$CACHE_DIR' -t $REGISTRY/$IMAGE_NAME:$TAG .'
                }
            }
            steps {
                container('buildah') {
                    sh 'buildah push $REGISTRY/$IMAGE_NAME:$TAG'
                }
            }
        }
    }
}
