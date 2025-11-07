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
                withSonarQubeEnv("sonar) {
                    sh 'sonar-scanner'
                }
            }
         }
    }
}
