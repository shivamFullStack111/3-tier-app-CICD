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
               sh '''
                wget https://github.com/jeremylong/DependencyCheck/releases/download/v8.0.2/dependency-check-8.0.2-release.zip -O dependency-check.zip
                unzip -o dependency-check.zip -d dependency-check-temp
                rm -rf dependency-check
                mv dependency-check-temp/dependency-check dependency-check
                rm -rf dependency-check-temp

                ./dependency-check/bin/dependency-check.sh \
                  --project "3-tier-backend" \
                  --scan . \
                  --format XML \
                  --out dependency-check-report.xml
            '''
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
