pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/adservice:latest ."
                    }
                }
            }
        }
        stage ('trivy'){
            steps{
                sh "trivy image chakalimurali/adservice:latest"
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/adservice:latest "
                    }
                }
            }
        }
    }
}
