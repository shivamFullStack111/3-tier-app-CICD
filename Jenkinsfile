pipeline {
    agent any

    environment {
        SONAR_SCANNER = "sonar-scanner-01"   // Tool wala naam 
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
                withSonarQubeEnv("Sonar") {   // 👈 Yahan "Sonar" wahi naam hona chahiye jo SonarQube server config me diya hai
                    sh '''
                        $SONAR_SCANNER/bin/sonar-scanner \
                          -Dsonar.projectKey=3-tier-app \
                          -Dsonar.projectName=3-tier-app \
                          -Dsonar.sources=.
                    '''
                }
            }
        }
    }
}
