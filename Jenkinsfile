pipeline {
    agent any
    
    stages {
        stage('Get Nodes') {
            steps {
                script {
                    sh 'whoami'
                    sh 'pwd'
                    sh 'ls -l'
                    sh 'export KUBECONFIG=/var/lib/jenkins/.kube/admin.conf'
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}
