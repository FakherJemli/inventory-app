pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Build Back-End') {
            steps {
                dir('inventory-back-end') {
                    sh 'mvn clean install -DskipTests'
                }
            }
        }

        stage('Build Front-End') {
            steps {
                dir('inventory-front-end') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
    }
}
