pipeline {
    agent any
    stages {
        stage('Build JAR') {
            steps {
                sh 'jar -cvf 645hw2.war *'
            }
        }
        stage('Build Docker image') {
            steps {
                sh 'docker build -t madhavnemani/sixfourfive .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh 'docker login -u madhavnemani -p {{pass}}'
            }
        }
        stage('Push Docker image') {
            steps {
                sh 'docker push madhavnemani/sixfourfive'
            }
        }
        stage('Copy kubeconfig') {
            steps {
                sh 'cp config ~/.kube/config'
            }
        }
        stage('Restart deployment') {
            steps {
                sh 'kubectl rollout restart deployment/sixfourfive'
            }
        }
    }
}
