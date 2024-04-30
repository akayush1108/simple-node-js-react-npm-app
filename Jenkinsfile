pipeline {
    agent any

    environment { 
        CI = 'true'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t my-node-app .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 --name my-node-container my-node-app'
                    sleep 10
                    sh 'docker logs my-node-container'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'npm install --save-dev cross-env'
                sh 'npm test'
            }
        }
        stage('Deliver') { 
            steps {
                sh 'npm run build'
                sh 'npm start &'
                sleep 1
                echo $! > .pidfile
            }
        }
    }
}
