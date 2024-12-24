pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'cd ../web'
                script {
                    dockerImage = docker.build("project1-web:${env.BUILD_NUMBER}")
                }
            } 
        }
        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://public.ecr.aws/c5o2a3r0/project1-repo', 'ecr:us-east-1:aws-credentials') {
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