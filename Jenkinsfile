pipeline {
  agent {
    label 'aws-deploy'
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

    stage('test-UI') {
      agent {
        docker {
          image 'node:17'
          args '-U root:root'
        }
      }

        steps {
            sh '''
        
        cd UI
        npm run
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
