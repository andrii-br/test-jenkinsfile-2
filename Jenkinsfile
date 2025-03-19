pipeline{
    agent any

    environment {
        IMAGE_NAME = "andriibry:my-app"
    }

    stages{
        stage("Copy repo"){
            steps{
                echo "========COPY REPO========"
                git branch: 'main', url: 'https://github.com/andrii-br/test-jenkinsfile-2.git'
            }
        }
        stage("Build docker image"){
            steps{
                echo "========Docker build========"
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage("Run container"){
            steps{
                echo "========Run container========"
                sh 'docker compose up -d'
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                    docker.withRegistry('', 'dockerhub-credentials'){
                        sh 'docker push $IMAGE_NAME'
                    }
                }
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
        stage("Deploy to server"){
            steps{
                sshagent([server]){
                    sh '''
                        ssh -o StrictHostKeyChecking=no server@192.168.100.4 "docker pull $IMAGE_NAME && docker run -d -p 80:80 $IMAGE_NAME"
                    '''
                }
            }
        }
    }
}
