#!groovy


pipeline {
    agent any
    stages {
        stage('Clone the repo') {
            steps {
                echo 'Cloning the repository:'
                git branch: 'main', url: 'https://github.com/t-donnenfeld/berthonweb'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t localhost:5000/les12/berthonweb:latest .'
            }
        }
        stage('Docker Push') {
            agent any
            environment {
                    DOCKER_REGISTRY_CREDS = credentials('c5c82df7-4d85-4778-ac39-c7937dfdd064')
            }
            steps {
                sh 'docker login -u $DOCKER_REGISTRY_CREDS_USR -p $DOCKER_REGISTRY_CREDS_PSW localhost:5000'
                sh 'docker push localhost:5000/les12/berthonweb:latest'
            }
        }
        stage('Docker Recreate') {
            agent any
            steps {
                sh 'docker-compose -f "/var/local/docker-compose.yml" pull'
                sh 'docker-compose -f "/var/local/docker-compose.yml" up --force-recreate --build -d'
                sh 'docker image prune -f'
            }
        }
    }
}
