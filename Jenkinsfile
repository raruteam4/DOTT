pipeline {
    agent any
    environment {
        EXECUTE = 'true'
    }
    
    tools {nodejs "node"}
    
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/raruteam4/DOTT'
            }
        }
        
        stage('Install Dependencies'){
            steps {
                sh 'npm install'
            }
        }
        
        stage ('SonarQube') {
            when {
                expression{env.EXECUTE}
            }
            steps {
                script {
                    def scannerHome = tool 'sonarqube';
                    withSonarQubeEnv("sonarqube") {
                        sh "${tool("sonarqube")}/bin/sonar-scanner \
                        -Dsonar.organization=raruteam4 \
                        -Dsonar.projectKey=raruteam4_DOTT \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=https://sonarcloud.io"
                    }
                }
            }
        }
        stage ('Test') {
            when {
                expression{!env.EXECUTE}
            }
            steps {
                sh 'npm test'
            }
        }
    }
}
