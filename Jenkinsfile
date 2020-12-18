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
                //sh 'npm install'
                sh 'npm install -D esm'
                //sh 'npm install babel-preset-env --save-dev'
            }
        }
        
        stage ('SonarQube') {
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
            steps {
                script{
                    try{
                        sh "npm test"
                    }
                    catch(exc){
                        echo "Error en test"
                    }
                }                    
            }
        }
    }
}
