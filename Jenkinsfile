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
                    dockerImageWeb = docker.build("project1-web:${env.BUILD_NUMBER}", "./web")
                    dockerImageCart = docker.build("project1-cart:${env.BUILD_NUMBER}", "./cart")
                }
            } 
        }
        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://992382444469.dkr.ecr.us-east-1.amazonaws.com/project1-web', 'ecr:us-east-1:aws-credentials') {
                    dockerImageWeb.push("${env.BUILD_NUMBER}")
                    dockerImageWeb.push("latest")

                    dockerImageCart.push("${env.BUILD_NUMBER}")
                    dockerImageCart.push("latest")
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