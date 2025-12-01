pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'ls -R .'
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
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        success {
            echo "✔ Build SUCCESSFUL"
        }
        failure {
            echo "❌ Build FAILED"
        }
    }
}
