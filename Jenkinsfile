pipeline {
    agent {
        label ("aws-deploy")
          }

    stages {
        stage('test auth') {
          agent{
            docker{
                image 'golang:alpine'
            }
          }
            steps {
                sh '''
            cd auth/scr/main
            go build 
            cd -
            ls -la
                '''
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
