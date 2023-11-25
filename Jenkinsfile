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
    stage('Prepare') {
      agent {
        label 'aws-deploy' // Replace 'your-dynamic-label' with the label for the dynamic agents
      }
      steps {
        script {
          // Download and install SonarScanner
          sh '''
            sudo apt update
            sudo apt install default-jre -y
            sudo mkdir /opt/sonar-scanner
            cd /opt/sonar-scanner
            sudo wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip
            sudo unzip sonar-scanner-cli-4.6.2.2472-linux.zip
          '''
        }
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
      agent any
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
