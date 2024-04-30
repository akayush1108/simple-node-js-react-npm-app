pipeline {
    agent any

    stages {
        stage('Creating a Docker image') {
            steps {
		echo "Building.."
                sh 'docker build -t react-app-image .'
            }
        }
        stage('Creating a Docker container') { 
            steps {
                sh 'docker run -p 8081:8080 react-app-image
            }
        }
    }
}
