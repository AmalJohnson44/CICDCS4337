pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure NodeJS is configured in Jenkins tools
    }

    environment {
        SONARQUBE_SERVER = 'SonarQube' // Use the name of your SonarQube server as configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Cloning the repository
                git url: 'https://github.com/AmalJohnson44/CICDemo.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Installing dependencies
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Running tests
                bat 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Building the project
                bat'npm run build'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Running SonarQube analysis
                withSonarQubeEnv('SonarQube') { // Use the SonarQube server name configured in Jenkins
                    bat'npm run sonar'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Add deployment steps here, e.g., deploy to a server
                echo 'Deploying application...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
