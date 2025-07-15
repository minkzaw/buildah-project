pipeline {
    agent any
    stages {
        stage ('Hello from Jenkins') {
            steps {
                sh 'echo "Hello World"'
            }
        }
        stage ('Build with buildah') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'bulidah-project',
                    usernameVariable: 'REGISTRY_USER',
                    passwordVariable: 'REGISTRY_PASS'
                )]) {
                    container('buildah') {
                        sh 'buildah login -u $REGISTRY_USER -p $REGISTRY_PASS quay.io'
                    }
                }
            }
        }
    }
}
