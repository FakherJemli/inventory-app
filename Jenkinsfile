pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                sh "ls -R ."
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
            echo "🎉 Build SUCCESS !"
        }
        failure {
            echo "❌ Build FAILED"
        }
    }
}
