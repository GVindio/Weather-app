pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timeout (time: 60, unit: 'MINUTES')
        timestamps()
      }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository from version control
                git 'https://github.com/GVindio/Weather-app.git'
            }
        }

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

        stage('Test weather') {
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
            steps {
                withSonarQubeEnv('SonarCloud') {
                    script {
                        sh 'sonar-scanner -Dsonar.projectKey=e9b32d2da2f5b630529008c76582d8b49e36d593 -Dsonar.organization=gvindio -Dsonar.sources=src'
                    }
                }
            }
        }
    }
}
