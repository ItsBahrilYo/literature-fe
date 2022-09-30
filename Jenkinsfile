def credential = 'aplikasi'
def server = 'bahril@27.112.78.215'
def directory = 'docker-fe/literature-frontend'
def branch = 'production'

pipeline{
    agent any
    stages{
        stage ('compose down &  pull'){
            steps{
                sshagent([credential]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    docker-compose down
                    docker system prune -f
                    cd ${directory}
                    git pull origin ${branch}
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker build'){
            steps{
                sshagent([credential]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose build
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker up'){
            steps{
                sshagent([credential]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose up -d
                    exit
                    EOF"""
                }
            }
        }
    }
}

