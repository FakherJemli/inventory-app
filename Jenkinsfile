pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                sh "ls -R ."
            }
        }

        stage('Build Back-End') {
            steps {
                dir('inventory-back-end') {
                    sh 'ls -l'
                    sh 'mvn clean install -DskipTests'
                }
            }
        }

        stage('Build Front-End') {
            steps {
                dir('inventory-front-end') {
                    sh 'ls -l'
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
