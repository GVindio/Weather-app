pipeline {
    agent any

    stages {
        stage('test auth') {
          agent{
            docker{
                image 'golang:alpine'
            }
          }
            steps {
                sh '''
            pwd
            ls -l
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
