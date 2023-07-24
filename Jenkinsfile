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
                        docker build -t nginx:$GIT_COMMIT  -f Dockerfile.main .
                        docker login nexus.wakatech.com:5001 --username $NEXUS_USER --password $NEXUS_PASSWORD
                        docker tag nginx:$GIT_COMMIT nexus.wakatech.com:5001/nginx:$GIT_COMMIT
                        docker push nexus.wakatech.com:5001/nginx:$GIT_COMMIT
                        export KUBECONFIG=/var/lib/jenkins/.kube/admin.conf
                        kubectl apply -f nginx-deploy.yaml
                        '''
                    }                    
                }
            }
        }
    }
}
