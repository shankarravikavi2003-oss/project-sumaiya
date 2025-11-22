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
    }
}
