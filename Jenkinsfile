pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'nodejs-lts', type: 'NodeJSInstallation'
        PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Anikeshsmn26/Cypress.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat 'npm install'
                }
            }
        }

        stage('Run Cypress Tests') {
            steps {
                script {
                    bat 'npx cypress run'
                }
            }
        }
    }

    post {
        always {
            junit 'cypress/results/*.xml'
            archiveArtifacts artifacts: 'cypress/screenshots/**/*, cypress/videos/**/*', allowEmptyArchive: true
        }
    }
}
