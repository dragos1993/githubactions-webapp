pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'dragos93/argocd-web-app:28'
                    reuseNode true
                }
            }
            steps {
                sh '''
                echo 'test'
                '''
            }
        }
    }
}