pipeline {
    agent any
    stages {
        stage("Checkout Repository") {
            steps {
                git credentialsId: 'jenk-docker-github6', url: 'https://github.com/DpkYdv887/jenkins-part2.git'
            }
        }
        stage("verifying tooling") {
            steps {
                sh '''
                    docker version
                    docker info
                    docker compose version
                    curl --version
                    jq --version
                '''
            }
        }
        stage("Prune Docker Data") {
            steps {
                sh 'docker system prune -a --volumes -f'
            }
        }
        stage("Start Container") {
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
            }
        }
        stage("Check Response") {
            steps {
                sh 'curl http://localhost'
            }
        }
    }
}
