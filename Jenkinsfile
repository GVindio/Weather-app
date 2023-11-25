pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository from version control
                git 'https://github.com/GVindio/Weather-app.git'
            }
        }

        stage('Build') {
            steps {
                // Build your project (e.g., Maven, Gradle, etc.)
                sh 'mvn clean install'
            }
        }

        stage('SonarQube analysis') {
            steps {
                // Run SonarQube scanner with the necessary parameters
                withSonarQubeEnv('SonarCloud') {
                    sh 'sonar-scanner -Dsonar.projectKey=e9b32d2da2f5b630529008c76582d8b49e36d593 -Dsonar.organization=gvindio -Dsonar.sources=src'
                }
            }
        }
    }
}
