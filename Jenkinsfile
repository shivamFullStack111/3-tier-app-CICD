pipeline {
    agent any

    environment {
        SONAR_HOME = tool "sonar-scanner-00"   // 👈 wahi naam jo Tools me diya
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
                withSonarQubeEnv("Sonar") {   // 👈 Global SonarQube server ka naam
                    sh "$SONAR_HOME/bin/sonar-scanner -Dsonar.projectKey=3-tier-app -Dsonar.projectName=3-tier-app -Dsonar.sources=."
                }
            }
        }

       stage('OWASP Dependency Check') {
    steps {
        dir('backend') {
              dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'dc-tool'
              dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
        }
    }
}

    }

    post {
        always {
            echo "Pipeline finished."
        }
    }
}
