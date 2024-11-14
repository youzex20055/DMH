pipeline {
    agent { label 'ubuntu-latest' } // Specify the agent (node) if necessary

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')  // Use Jenkins credentials manager
        SONAR_HOST_URL = credentials('SONAR_HOST_URL')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from the repository
                checkout scm
            }
        }

        stage('Run SonarQube Scan') {
            steps {
                // Run SonarQube scan using SonarScanner CLI
                withSonarQubeEnv('SonarQube Server') { // Use the configured SonarQube server name
                    sh '''
                    sonar-scanner \
                        -Dsonar.projectKey=my_project_key \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=$SONAR_HOST_URL \
                        -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
