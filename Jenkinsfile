pipeline {
    agent any
    
    stages {
        stage('Get Nodes') {
            steps {
                script {
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}
