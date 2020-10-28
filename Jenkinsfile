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
                cd helm
                cd python-chart
                curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
                chmod +x ./kubectl
                helm install --name python-chart . 
                ''' 
            }
        }
    }
}