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
                sh 'docker run -dp 81:80 react-app-image'
            }
        }
    }
}
