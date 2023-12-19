pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins_aws_key_id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins_aws_key_secret')
    } 
    
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
                bat (script:  'aws configure set region us-east-1',returnStdout: true);
                bat(script: 'kubectl config use-context arn:aws:eks:us-east-1:872333639793:cluster/DevOps-Eks --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
                bat(script: 'kubectl apply -f k8s.yml --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
                bat(script: 'kubectl rollout restart deployment app-deployment --kubeconfig=%KUBE_PATH_CONFIG%', returnStdout: true);
            }
        }
    }
}


