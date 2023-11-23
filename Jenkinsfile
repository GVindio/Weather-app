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
                sh '''
                    cd auth/src/main
                    go build
                    cd -
                    ls -la
                '''
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
                sh '''
                    cd UI
                    npm run
                '''
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
                sh '''
                    cd weather
                    pip3 install -r requirements.txt
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQubeScanner') {
                        sh '''
                            sonar-scanner \
                            -Dsonar.host.url=http://54.165.247.157:9000/ \
                            -Dsonar.login=squ_4d13e8843d63258727c69d45606c94fddab77e1e
                        '''
                    }
                }
            }
        }
    }


    post {
        always {
            // Additional post-build actions or clean-up steps
            echo 'Always executing post-build actions...'
        }
    }
}
