pipeline {
    agent any

    tools {
        nodejs "node20"
    }

    environment {
        BACKEND_DIR = "inventory-back-end"
        FRONTEND_DIR = "inventory-front-end"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/FakherJemli/inventory-app.git'
                sh 'ls -R .'
            }
        }

        stage('Build Back-End (Gradle)') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh "chmod +x ./gradlew"
                    sh "./gradlew clean build"
                }
            }
        }

        stage('Build Front-End (Angular)') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh "npm install"
                    sh "npm run build"
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
