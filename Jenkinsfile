pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool "sonar-scanner-01"
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
                withSonarQubeEnv("Sonar") {   // 👈 SonarQube server ka naam
                    sh '''
                        $SONAR_SCANNER_HOME/bin/sonar-scanner \
                          -Dsonar.projectKey=3-tier-app \
                          -Dsonar.projectName=3-tier-app \
                          -Dsonar.sources=.
                    '''
                }
            }
        }
    }
}
