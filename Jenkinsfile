pipeline {
    agent any
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
                sh 'docker login -u tejaswi251100 -p {{docker_pass}}'
            }
        }
        stage('Push Docker image') {
            steps {
                sh 'docker push tejaswi251100/tejaswidevi'
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
