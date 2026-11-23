pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/checkoutservice:latest ."
                    }
                }
            }
        }
        stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/checkoutservice:latest" >> checkoutservice.txt
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/checkoutservice:latest "
                    }
                }
            }
        }
    }
}
