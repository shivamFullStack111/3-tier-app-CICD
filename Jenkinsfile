pipeline {
    agent any

    environment {
        SONAR_HOME = tool "sonar-scanner-01"   // Jenkins Tools me diya hua naam
    }

    stages {
        stage('Code Checkout') {
            steps {
                git branch: "main", url: 'https://github.com/shivamFullStack111/3-tier-app-CICD'
                echo 'Code clone successful'
                sh 'ls'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv("Sonar") {   // Jenkins Global SonarQube server ka naam
                    sh """
                        $SONAR_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=3-tier-app \
                        -Dsonar.projectName=3-tier-app \
                        -Dsonar.sources=.
                    """
                }
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                dir('backend') {
                    sh '''
                        wget https://github.com/jeremylong/DependencyCheck/releases/download/v8.0.2/dependency-check-8.0.2-release.zip -O dependency-check.zip
                        unzip -o dependency-check.zip -d dependency-check
                        ./dependency-check/bin/dependency-check.sh --project "3-tier-backend" --scan . --out owasp-report
                    '''
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: 'backend/owasp-report/**', allowEmptyArchive: true
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

