pipeline {
  agent {
    label 'aws-deploy'
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
            id
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
