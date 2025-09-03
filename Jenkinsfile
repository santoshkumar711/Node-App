stages {
    stage('Checkout') {
        steps {
            // This step checks out the source code from your Git repository.
            // It ensures the latest code, including the Dockerfile, is available.
            git branch: 'main', url: 'https://github.com/santoshkumar711/Node-App.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            // This command builds the Docker image. The '.' specifies that
            // the Dockerfile is in the current directory (the root of the checked-out repo).
            // This stage will only succeed if the Dockerfile exists in your Git repository.
            sh 'docker build -t nodeapp:v1 .'
        }
    }

    stage('Stop Existing Container') {
        steps {
            // This is a crucial step for continuous deployment. It first checks
            // if a container with the name 'nodeapp' is running.
            // If it finds one, it stops and removes it to avoid conflicts.
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
            // This command runs a new Docker container in detached mode (-d),
            // maps port 80 on the host to port 3000 inside the container,
            // and names the container 'nodeapp'.
            sh 'docker run -d -p 80:3000 --name nodeapp nodeapp:v1'
        }
    }
}

