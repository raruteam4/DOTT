pipeline {
    agent any
    environment {
        EXECUTE = 'true'
    }
    
    tools {nodejs "node"}
    
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/raruteam4/mocha_testing'
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
                sh 'echo " Esta vaina"'
            }
        }
        stage ('Test') {
            when {
                expression{}
            }
            steps {
                sh 'npm test -- ipv4validation.js'
                sh 'npm test'
            }
        }
    }
}
