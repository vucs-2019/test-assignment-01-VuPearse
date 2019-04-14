pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'Most Recent Node') {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                nodejs(nodeJSInstallationName: 'Most Recent Node') {
                    sh 'npm run test'
                }
            }
        }
    }
}