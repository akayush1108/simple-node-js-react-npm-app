pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('hello-world-react-app')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    docker.image('hello-world-react-app').run('-p 3000:3000')
                }
            }
        }
    }
}
