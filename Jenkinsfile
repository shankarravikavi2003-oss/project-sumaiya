pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/shankarravikavi2003-oss/project-sumaiya.git'
            }
        }
         stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("sonar") {
                    sh 'sonar-scanner'
                }
            }
         }
         stage('Build the Docker image') {
            steps {
                sh 'docker build -t newimage .'
                }
         }
         stage('Image Scan') {
            steps {
                sh 'trivy image newimage:latest > report.txt'
                }
            }
         stage('Deploy') {
            steps {
                sh '''
                    sed -i "s|_IMAGE_|newimage:latest|g" pod.yaml
                    kubectl apply -f pod.yaml    
                '''
            }
         }
    }
}
