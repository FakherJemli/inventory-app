pipeline {
    agent any

    tools {
        jdk 'JDK17'            // Ton installation JDK (nom exact dans Jenkins)
        nodejs 'Node20'        // NOM EXACT que tu viens d’ajouter dans Global Tool Config
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Back-End (Gradle)') {
            steps {
                dir('inventory-back-end') {
                    sh 'chmod +x ./gradlew'
                    sh './gradlew clean build'
                }
            }
        }

        stage('Build Front-End (Angular)') {
            steps {
                dir('inventory-front-end') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        success {
            echo "✔️ Build SUCCESS"
        }
        failure {
            echo "❌ Build FAILED"
        }
    }
}
