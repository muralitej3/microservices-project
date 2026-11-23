pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/productcatalogservice:latest ."
                    }
                }
            }
        }
         stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/productcatalogservice:latest"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/productcatalogservice:latest "
                    }
                }
            }
        }
    }
}
