pipeline {
    agent {
        docker {
            image 'node:16-alpine'
            args '-p 3000:3000'
        }
    }
    environment { 
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
		echo "Building.."
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deliver') { 
            steps {
                sh 'npm run build'
                sh 'npm start &'
                sleep 1
                echo "\$! > .pidfile"
            }
        }
    }
}
