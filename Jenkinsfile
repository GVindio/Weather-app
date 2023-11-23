pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from the repository
                git url: 'https://github.com/GVindio/Weather-app.git'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner' // Make sure 'SonarQubeScanner' is configured in Jenkins Global Tool Configuration
                    withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                        sh """
                            sonar-scanner \
                            
                            -Dsonar.host.url=http://54.165.247.157:9000/ \
                            -Dsonar.login=squ_4d13e8843d63258727c69d45606c94fddab77e1e
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            // Additional post-build actions or clean-up steps
        }
    }
}
