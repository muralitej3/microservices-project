pipeline { 
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/shippingservice:latest ."
                    }
                }
            }
        }
        stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/shippingservice:latest >> shipping.txt"
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/shippingservice:latest "
                    }
                }
            }
        }
    }
}
