pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('src') {

                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker build -t chakalimurali/cartservice:latest ."
                    }
                        }
                }
            }
        }

         stage('Trivy Scan') {
            steps {
                sh "trivy image chakalimurali/cartservice:latest" >> cart.txt
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker', toolName: 'docker') {
                        sh "docker push chakalimurali/cartservice:latest "
                    }
                }
            }
        }
    }
}
