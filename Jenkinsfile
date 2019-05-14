
pipeline {
    agent any
    stages {

    stage('Clone Repo') {
        sh 'rm -rf dockertest1'
        sh 'git clone https://github.com/Shayaan2018/dockertest1.git'
    }

    stage('Build Docker Image') {
        sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
        sh ' cp  /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
        sh 'docker build -t shayaan2018/pipelinetest:v1 .'
    }

    stage('Push Image to Docker Hub') {
     sh 'docker push shayaan2018/pipelinetest:v1'
    }

    stage('Deploy to Docker Host') {
     sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 --network ansible_nw shayaan2018/pipelinetest:v1'
    }

    stage('Check WebApp Rechability') {
     sh 'curl http:// ec2-18-234-70-204.compute-1.amazonaws.com:9000'
    }

  }

}
