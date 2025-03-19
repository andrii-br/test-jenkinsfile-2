pipeline {
    agent any

    environment {
        IMAGE_NAME = "andriibry/my-app:latest"
    }

    stages {
        stage("Copy repo") {
            steps {
                echo "========COPY REPO========"
                git branch: 'main', url: 'https://github.com/andrii-br/test-jenkinsfile-2.git'
            }
        }
        stage("Build docker image") {
            steps {
                echo "========Docker build========"
                sh "docker build -t ${env.IMAGE_NAME} ."
            }
        }
        stage("Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                        sh "docker push ${env.IMAGE_NAME}"
                    }
                }
            }
        }
        stage("Deploy to server") {
            steps {
                sshagent(['server']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no server@192.168.100.4 "
                        docker pull ${env.IMAGE_NAME} &&
                        docker stop my-app || true &&
                        docker rm my-app || true &&
                        docker run -d --name my-app -p 80:80 ${env.IMAGE_NAME}"
                    '''
                }
            }
        }
    }
}
