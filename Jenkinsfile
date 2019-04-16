pipeline {
    agent any

    stages {
        stage('Pre work') {
            steps {
                script {
                    sh 'printenv'
                    properties([[$class: 'GithubProjectProperty',
                                projectUrlStr: GIT_URL]])
                }
            }
        }
        stage('Pull In Test Repo'){
            steps {
                sh 'git submodule update --init --recursive'
            }
        }
        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'Most Recent Node') {
                    dir("test-assignment-01-tests") {
                        sh 'npm install'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                nodejs(nodeJSInstallationName: 'Most Recent Node') {
                    script {
                        dir("test-assignment-01-tests") {
                            env.TEST_RESULTS = sh 'npm run test'
                        }             
                    }
                }
            }
        }
    }  
    post {
        always {
            dir("test-assignment-01-tests") {
                sh 'ls -la'
                junit 'test-assignment-01-tests/jenkins-test-results.xml'
                step([$class: 'GitHubIssueNotifier',
                    issueAppend: true,
                    issueLabel: '',
                    issueTitle: "$JOB_NAME $BUILD_DISPLAY_NAME failed",
                    issueBody: env.TEST_RESULTS])
            }      
        }
    }
}