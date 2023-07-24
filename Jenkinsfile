pipeline {
    agent any
    
    stages {
        stage('Get Nodes') {
            steps {
                script {
                    sh 'whoami'
                    sh 'pwd'
                    sh 'ls -l'
                    sh 'export KUBECONFIG=/var/lib/jenkins/workspace/dev/.kube/admin.conf'
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}
