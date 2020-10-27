pipeline {
    agent { 
        kubernetes{
            label 'jenkins-slave'
        }
    }
    stages {
        stage('Helm deployment') {
            steps{
                sh(script: """
                    git clone https://github.com/wahaj123/helm.git
                """, returnStdout: true)
                sh script: '''
                #!/bin/bash 
                curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
                chmod +x ./kubectl
                cd python-chart
                ./kubectl apply -f rbac-config.yaml
                helm init --service-account tiller --history-max 200 
                helm install --name python-chart . 
                ''' 
            }
        }
    }
}