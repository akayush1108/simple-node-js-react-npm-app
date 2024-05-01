pipeline {
    agent any

    stages {
	stage('Preparation') {
	    steps {
		// Clean before build
                cleanWs()
                // We need to explicitly checkout from SCM here
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
    post {
        // Clean after build
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true,
                    patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                               [pattern: '.propsfile', type: 'EXCLUDE']])
        }
    }
}
