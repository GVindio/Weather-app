pipeline {
    agent {
        label "aws-deploy"
    }

    stages {
        stage('test auth') {
            agent {
                docker {
                    image 'golang:alpine'
                    args '-u root'
                }
            }
            steps {
                script {
                    sh '''
                        
                        cd auth/src/main
                        go build
                        cd -
                        ls -la
                    '''
                }
            }
        }

        stage('Hello-2b') {
            steps {
                sh '''
                    ls
                    pwd
                '''
            }
        }

        stage('Hello-3c') {
            steps {
                sh '''
                    ls
                    pwd
                '''
            }
        }
    }
}

