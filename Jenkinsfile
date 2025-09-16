pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('Sonar')  // Jenkins me stored Sonar token
        SONAR_HOST_URL = 'http://172.16.210.130:9000' // SonarQube server ka URL
    }

    tools {
        sonarScanner 'Sonar-scanner'   // 👈 yahan wahi naam likho jo Tools me configure kiya tha
    }

    stages {
        stage('Code pulling') {
            steps {
                git branch: "main", url: 'https://github.com/shivamFullStack111/3-tier-app-CICD'
                echo 'Code clone successful'
                sh 'ls'
            }
        }

        stage('Sonarqube scanning') {
            steps {
                withSonarQubeEnv('Sonar') {   // 👈 yahan "Sonar" wahi naam hai jo Jenkins Global SonarQube servers me diya tha
                    sh """
                    ${tool 'Sonar-scanner'}/bin/sonar-scanner \
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
