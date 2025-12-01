pipeline {
    agent any

    tools {
        maven 'Maven'     // Maven tool name configuré dans Jenkins
        nodejs 'NodeJS'   // NodeJS tool name configuré dans Jenkins
    }

    stages {

        stage('Checkout code') {
            steps {
                echo '📥 Cloning repository...'
                checkout scm
            }
        }

        stage('Verify folders') {
            steps {
                echo "📂 Listing workspace content..."
                sh "ls -R ."
            }
        }

        stage('Build Back-End') {
            steps {
                echo '🚀 Building Spring Boot backend...'
                dir('inventory-back-end') {
                    sh 'ls -l'
                    sh 'mvn -version'
                    sh 'mvn clean install -DskipTests'
                }
            }
        }

        stage('Build Front-End') {
            steps {
                echo '🌐 Building Angular front-end...'
                dir('inventory-front-end') {
                    sh 'ls -l'
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        always {
            echo '🏁 Pipeline finished'
        }
        success {
            echo '✅ BUILD SUCCESSFUL'
        }
        failure {
            echo '❌ BUILD FAILED'
        }
    }
}
