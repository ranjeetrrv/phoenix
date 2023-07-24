pipeline {
    agent any
    options {
            buildDiscarder(logRotator(numToKeepStr: "5"))
            }
    stages {
            stage('get-env') {
                environment {
                    NEXUS_FILE = credentials('nexus') 
                    NEXUS_USER = sh (script: 'cat $NEXUS_FILE | grep NEXUS_USER | cut -d "=" -f 2', returnStdout: true).trim()
                    NEXUS_PASSWORD = sh (script: 'cat $NEXUS_FILE | grep NEXUS_PASSWORD | cut -d "=" -f 2', returnStdout: true).trim()         
                }
                steps {
                    sshagent(credentials: ['jenkins-key'])
                    {
                       {
                       sh '''
                        export KUBECONFIG=/var/lib/jenkins/.kube/admin.conf
                        kubectl get nodes
                        '''
                    }                    
                }
            }
        }
    }
}
