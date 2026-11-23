pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/loadgenerator:latest ."
                    }
                }
            }
        }
         stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/loadgenerator:latest >> load.txt"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/loadgenerator:latest"
                    }
                }
            }
        }
    }
}
