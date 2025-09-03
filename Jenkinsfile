pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodeapp:latest .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh '''
                if [ $(docker ps -q -f name=nodeapp) ]; then
                    docker stop nodeapp
                    docker rm nodeapp
                fi
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 80:3000 --name nodeapp nodeapp:latest'
            }
        }
    }
}
