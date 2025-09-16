pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('Sonar') // Jenkins me saved Sonar token
        SONAR_HOST_URL = 'http://172.16.210.130/:9000' // SonarQube server URL
    }

    stages {

        // Stage 1: Code Pulling
        stage('Code pulling') {
            steps {
                git branch: "main", url: 'https://github.com/shivamFullStack111/3-tier-app-CICD'
                echo 'Code clone successful'
                sh 'ls'    
            }
        }

        // Stage 2: SonarQube Scan
        stage('Sonarqube scanning') {
            steps {
                echo 'Running SonarQube scan...'

                // Jenkins me configured SonarQube server ka environment use kar rahe hain
                withSonarQubeEnv('Sonar') {
                    sh """
                    Sonar-scanner \
                    -Dsonar.projectKey=3-tier-app \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=$SONAR_HOST_URL \
                    -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }
    }
}
