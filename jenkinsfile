pipeline {
    agent any
    
    stages{
        stage ('SCM'){
            steps{
                git branch: 'master' , url: 'https://github.com/stevelopezcGT/devops-dotnet-account-23'
            }
        }
        
        stage('Builder Image'){
            steps {
                bat (script: 'dir', returnStdout:true);
                
                bat(script: 'docker build -t stevelopez/devops-ms-account .', returnStdout:true);
                bat(script: 'docker push stevelopez/devops-ms-account', returnStdout:true );
            }
        }
        
        stage ('Deploy AKS') {
            steps{
                bat (script: 'az login --service-principal --username 4e4bf419-d33e-4fb7-bd94-e832f59878db --password NWx8Q~0MY9QXL.uSsG163KKJcfTCKCItPNLRYaCt --tenant b8272504-4b38-40a2-829d-1c777a9de7bb', returnStdout:true);
                bat (script: 'az account set --subscription d4cd5845-6cc6-45c9-a910-599e8d6bd7cb', returnStdout:true);
                bat(script: 'kubectl config use-context polyglot-cluster-azure --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
                bat(script: 'kubectl apply -f k8s.yml --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
                bat(script: 'kubectl rollout restart deployment app-deployment --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
            }
        }
    }
}