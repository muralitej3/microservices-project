pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/paymentservice:latest ."
                    }
                }
            }
        }
         stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/paymentservice:latest >> payment.txt"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/paymentservice:latest "
                    }
                }
            }
        }
    }
}
