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
            steps {
                withCredentials([usernamePassword(credentialsId: 'c5c82df7-4d85-4778-ac39-c7937dfdd064', passwordVariable: 'registryPassword', usernameVariable: 'registryUser')]) {
                    sh "docker login -u ${env.registryUser} -p ${env.registryPassword}"
                    sh 'docker push localhost:5000/les12/berthonweb:latest'
                }
            }
        }
    }
}
