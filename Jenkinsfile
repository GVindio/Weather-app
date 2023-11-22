pipeline {
  agent {
    label 'aws-deploy'
  }
  
  options {
       buildDiscarder(logRotator(numToKeepStr: '5'))
       disableConcurrentBuilds()
       timeout (time: 60, unit: 'MINUTES')
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

        stage('SonarQube analysis') {
         agent {
            docker {
              image 'sonarsource/sonar-scanner-cli:4.7.0'
                }
               }
               environment {
        CI = 'true'
        //  scannerHome = tool 'Sonar'
        scannerHome='/opt/sonar-scanner'
    }
            steps{
                withSonarQubeEnv('Sonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }    

     }

}
