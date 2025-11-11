pipeline {
    agent any
    tools {
        sonar-scanner
    }
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/shankarravikavi2003-oss/project-sumaiya.git'
            }
        }
         stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("sonar") {
                    script {
                def scannerHome = tool 'sonar-scanner'
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=k8-fastapi-project -Dsonar.sources=. -Dsonar.host.url=http://43.205.117.106:9000 -Dsonar.login=sonar"
                }
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
