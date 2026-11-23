pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/currencyservice:latest ."
                    }
                }
            }
        }
        stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/currencyservice:latest >> currency.txt"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/currencyservice:latest "
                    }
                }
            }
        }
    }
}
