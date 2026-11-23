pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/recommendationservice:latest ."
                    }
                }
            }
        }
         stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/recommendationservice:latest"
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/recommendationservice:latest "
                    }
                }
            }
        }
    }
}
