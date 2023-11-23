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
        // ... (Test auth, Test UI, Test Weather, SonarQube Analysis stages)

        stage('Final Steps') {
            steps {
                // Perform any final post-build actions or clean-up steps here
                echo 'Performing additional post-build actions...'
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
