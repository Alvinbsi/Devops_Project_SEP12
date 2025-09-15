pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Iam-mithran/SaturdayProject.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t devopsfirstcicd /var/lib/jenkins/workspace/Devops_First_CI_CD'
                sh 'sudo docker tag devopsfirstcicd alvinselva/devopsfirstcicd:latest'
                sh 'sudo docker tag devopsfirstcicd alvinselva/devopsfirstcicd:${BUILD_NUMBER}'
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
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/Devops_First_CI_CD/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}