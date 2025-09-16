pipeline {
    agent any

    stages {
        stage('Code pulling') {
            steps {
                git branch: "main", url: 'https://github.com/shivamFullStack111/3-tier-app-CICD'
                echo 'Code clone successfull '
                sh 'ls'    
            }
        }
        
    }
}
