pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Ravikodekal/k8s_jenkins_integration']]])
                sh 'cd /var/lib/jenkins/workspace/k8s-dockerhub'
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t ravikodekal/assignment:java1 .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   sh 'docker login -u username -p password'
                    sh 'docker push ravikodekal/assignment:java1'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfig')
                }
            }
        }
    }
}
