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
    }
}
