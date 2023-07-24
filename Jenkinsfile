pipeline {
    agent any
    
    stages {
        stage('Get Nodes') {
            steps {
                script {
                    sh 'export KUBECONFIG=/var/lib/jenkins/.kube/admin.conf'
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}
