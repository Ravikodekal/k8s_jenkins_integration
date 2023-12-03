pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Ravikodekal/k8s_jenkins_integration.git']])
            }
        }
        stage('Build docker image'){
            steps{
                script{
                     sh 'docker build -t ravikodekal:java-assign .'
                }
            }
        }
        stage('Push image to dockerhub'){
            steps{
                script{
                   sh 'docker login -u {enterYourDockerhubUser} -p {enterYourDockerhubPassword}'
                    sh 'docker push ravikodekal:java-assign'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy(configs: 'deploymentservice.yaml',kubeconfigId: 'kubernetes')
                }
            }
        }
    }
}
