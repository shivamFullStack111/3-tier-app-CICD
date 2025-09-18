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
stage('OWASP Dependency Check (OWASP scanning)') {
    steps {
        dir('backend') {
            // DIRECT inline token (example only) - not recommended
            dependencyCheck additionalArguments: "--scan ./ --nvdApiKey 553b2524-8b68-44dd-8619-99fbd45c89f1", odcInstallation: 'dc-tool'
            dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
        }
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
