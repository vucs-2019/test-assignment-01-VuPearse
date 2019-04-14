pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                nodejs() {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                nodejs() {
                    sh 'npm run test'
                }
            }
        }
    }
}