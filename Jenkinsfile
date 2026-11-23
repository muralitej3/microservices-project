pipeline {
    agent any

    stages {
        stage('Deploy') {
            when { branch 'main' }   // change 'main' to your branch name
            steps {
                sh '''
                    if docker compose version >/dev/null 2>&1; then
                        C="docker compose"
                    else
                        C="docker-compose"
                    fi
                    $C -f docker.yml pull
                    $C -f docker.yml up -d --remove-orphans
                    $C -f docker.yml ps
                '''
            }
        }
    }
}
