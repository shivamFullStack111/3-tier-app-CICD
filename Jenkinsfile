pipeline {
    agent any

    environment {
       SONAR_HOME = tool "sonar-scanner-01"
        
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
                withSonarQubeEnv("sonar-scanner-01") {   // 👈 yahan "Sonar" wahi naam hai jo Jenkins Global SonarQube servers me diya tha
                    sh "$SONAR_HOME/bin/sonar-scanner -Dsonar.projectName=3-tier-app -Dsonar.projectKey=3-tier-app" 
                }
            }
        }
    }
}
