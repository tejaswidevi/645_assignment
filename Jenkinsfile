pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
    }
    stages {
        stage('Build JAR') {
            steps {
                sh 'jar -cvf tej123.war *'
            }
        }
        stage('Build Docker image') {
            steps {
                sh 'docker build -t tejaswi251100/tejaswidevi .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-id', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                }
            }
        }
        stage('Push Docker image') {
            steps {
                sh 'docker push tejaswi251100/tejaswidevi'
            }
        }
        stage('Copy kubeconfig') {
            steps {
                sh 'cp ./config ~/.kube/config'
            }
        }
        stage('Restart deployment') {
            steps {
                sh 'kubectl rollout restart deployment/a'
            }
        }
    }
}
