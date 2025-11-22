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
                sh '/opt/sonar-scanner/bin/sonar-scanner'
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
         stage('Push to ECR') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'ecrtoken']]) {
                    sh '''
                        aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 889966879746.dkr.ecr.eu-north-1.amazonaws.com
                        docker tag newimage:latest 889966879746.dkr.ecr.eu-north-1.amazonaws.com/myrepo:latest
                        docker push 889966879746.dkr.ecr.eu-north-1.amazonaws.com/myrepo:latest
                    '''
                    }
                }
            }
        stage('Deploy') {
            steps {
                sh '''
                    sed -i "s|_IMAGE_|889966879746.dkr.ecr.eu-north-1.amazonaws.com/myrepo:latest|g" pod.yaml
                    kubectl apply -f pod.yaml    
                '''
            }
        }
    }
}
