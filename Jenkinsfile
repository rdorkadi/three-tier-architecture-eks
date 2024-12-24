pipeline {
    agent any
    stages {
        stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("project1-web:${env.BUILD_NUMBER}", "./web")
                }
            } 
        }
        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://992382444469.dkr.ecr.us-east-1.amazonaws.com/private-project1', 'ecr:us-east-1:aws-credentials') {
                    dockerImage.push("${env.BUILD_NUMBER}")
                    dockerImage.push("latest")
                }
            }
        }
        // stage('Deploy') {
        //     steps{
        //         install aws-cli
        //         aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
        //         aws eks update-kubeconfig --name EKS-Cluster-name --region us-east-1
        //     }
        //     steps {
        //         install helm
        //         helm install --set repo=ECRRepo project1-release ../project1-helm
                
        //     }
        // }
    }
}
}