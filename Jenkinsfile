pipeline {
    agent {
        label 'aws-deploy'
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timeout(time: 60, unit: 'MINUTES')
        timestamps()
    }

    stages {
        stage('Test auth') {
            agent {
                docker {
                    image 'golang:alpine'
                    args '-u root:root'
                }
            }
            steps {
                script {
                    sh '''
                        id
                        cd auth/src/main
                        go build
                        cd -
                        ls -la
                    '''
                }
            }
        }

        stage('Test UI') {
            agent {
                docker {
                    image 'node:17'
                    args '-u root:root'
                }
            }
            steps {
                script {
                    sh '''
                        cd UI
                        npm install
                        npm run
                    '''
                }
            }
        }

        stage('Test Weather') {
            agent {
                docker {
                    image 'python:3.8-slim-buster'
                    args '-u root:root'
                }
            }
            steps {
                script {
                    sh '''
                        cd weather
                        pip3 install -r requirements.txt
                    '''
                }
            }
        }

        stage('SonarQube analysis') {
            agent {
                docker {
                    image 'sonarsource/sonar-scanner-cli:4.7.0'
                }
            }
            environment {
                CI = 'true'
                SCANNER_HOME = '/opt/sonar-scanner'
            }
            steps {
                script {
                    sh "${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=35f9234a979911dc3387f26bbf4b8aab09f38d3a"
                }
            }
        }
    }
}
