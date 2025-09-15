pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/Alvinbsi/Devops_Project_SEP12.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'docker build -t devopsfirstcicd /var/lib/jenkins/workspace/Devops_First_CI_CD'
                sh 'docker tag devopsfirstcicd alvinselva/devopsfirstcicd:latest'
                sh 'docker tag devopsfirstcicd alvinselva/devopsfirstcicd:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push alvinselva/devopsfirstcicd:latest'
                sh 'sudo docker image push alvinselva/devopsfirstcicd:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/Devops_First_CI_CD/deployment.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}