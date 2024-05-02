// Declarative pipeline
pipeline {
    agent {
        node {
            label 'linux docker frontend'
        }
    }
    stages {
	stage('Preparation') {
	    steps {
                cleanWs()
                checkout scm
	    }
	}
        stage('Creating a Docker image') {
            steps {
		echo "Building.."
                sh 'docker build -t react-app-image .'
            }
        }
        stage('Creating a Docker container') { 
            steps {
                sh 'docker run -dp 3001:3000 react-app-image'
            }
        }
    }
}


// Scripted pipeline
// node {
//     stage('Preparation') {
//         cleanWs()
//         checkout scm
//     }

//     stage('Creating a Docker image') {
//         echo "Building.."
//         sh 'docker build -t react-app-image .'
//     }

//     stage('Creating a Docker container') {
//         sh 'docker run -dp 3001:3000 react-app-image'
//     }
// }
