pipeline {
    agent { label 'kube-masternode' }
    stages {
        stage('Clone Source Code') {
            steps {
                sh '''
                if [ -d wordpress-bp ]
                then
                    cd wordpress-bp && git pull
                else 
                    git clone https://github.com/rafli024/wordpress-bp.git
                fi
                '''
            }
        }
        
        stage('Clone CICD Repo'){
            steps{
                sh '''
                    cd $WORKSPACE && ls -ltr
                '''
            }
        }
        
        stage('Deploy to K8S'){
            steps{
                sh'''
                    cd $WORKSPACE    
                    kubectl apply -f .              
                    kubectl describe deployments/wordpress-deploy
                    kubectl get pods -A
                '''
            }
        }
    }
}