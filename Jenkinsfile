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
                // Install dependencies using npm
                script {
                    dir("${env.WORKSPACE}") {
                        bat 'npm install'
                    }
                }
            }
        }

        stage('Run Cypress Tests') {
            steps {
                // Run Cypress tests
                script {
                    dir("${env.WORKSPACE}") {
                        bat 'npx cypress run'
                    }
                }
            }
        }
    }

    post {
        always {
            node {
                // Archive the test results
                junit 'cypress/results/*.xml'
                // Archive screenshots and videos
                archiveArtifacts artifacts: 'cypress/screenshots/**/*, cypress/videos/**/*', allowEmptyArchive: true
            }
        }
    }
}
