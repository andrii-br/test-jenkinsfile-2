pipeline{
    agent any

    stages{
        stage("Copy repo"){
            steps{
                echo "========COPY REPO========"
                git branch: 'main', url: 'https://github.com/andrii-br/test-jenkinsfile-2.git'
            }
        }
        stage("Docker build for app.js"){
            steps{
                echo "========Docker build========"
                sh 'docker build .'
            }
        }
        stage("Run container"){
            steps{
                echo "========Run container========"
                sh 'docker compose up -d'
            }
        }
        stage("TEST"){
            steps{
                echo "========TEST========"
                sh 'sleep 7'
                sh 'docker ps'
                sh 'curl -i http://localhost:3000'
            }
        }
        stage("Stop docker container"){
            steps{
                echo "=====Stop docker container======"
                sh 'docker compose down'
            }
        }
    }
}
