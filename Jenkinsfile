pipeline {
    agent any

    stages {
        stage('Start Jenkins Container') {
            steps {
                script {
                    // Pull the Jenkins Docker image
                    docker.image('jenkins/jenkins').pull()

                    // Run the Jenkins container
                    docker.image('jenkins/jenkins').run('-d -p 8080:8080 -p 50000:50000 --name jenkins')

                    // Wait for Jenkins to start (optional)
                    sh 'sleep 30' // Adjust the sleep time as needed
                }
            }
        }

        // Existing stages from your Jenkinsfile
        stage('Build') {
            steps {
                sh 'mkdir -p ~/.npm'
                sh 'chown -R 113:118 ~/.npm'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }

        stage('Stop Jenkins Container') {
            steps {
                script {
                    // Stop and remove the Jenkins container after the build is complete
                    docker.image('jenkins/jenkins').stop()
                    docker.image('jenkins/jenkins').remove(force: true)
                }
            }
        }
    }
}
