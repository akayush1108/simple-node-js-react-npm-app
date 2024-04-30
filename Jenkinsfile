pipeline {
    agent any

    stages {
        stage('Start Jenkins Container') {
            steps {
                script {
                    docker.image('jenkins/jenkins').pull()
                    docker.image('jenkins/jenkins').run('-d -p 8888:8080 -p 50000:50000 --name jenkins2')
                    sh 'sleep 30' 
                }
            }
        }
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
                // input message: 'Finished using the web site? (Click "Proceed" to continue)'
                // sh './jenkins/scripts/kill.sh'
            }
        }

        // stage('Stop Jenkins Container') {
        //     steps {
        //         script {          
        //             docker.image('jenkins/jenkins').stop()
        //             docker.image('jenkins/jenkins').remove(force: true)
        //         }
        //     }
        // }
    }
}
