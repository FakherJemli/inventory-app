pipeline {
    agent any

    tools {
        maven 'Maven'   // Maven tool configured in Jenkins
        nodejs 'NodeJS' // NodeJS tool configured in Jenkins
    }

    stages {

        /* === CLONE === */
        stage('Checkout') {
            steps {
                echo "📥 Cloning inventory-app repository..."
                git branch: 'main', url: 'https://github.com/FakherJemli/inventory-app.git'
            }
        }

        /* === BACKEND === */
        stage('Backend - Build') {
            steps {
                dir('inventory-back-end') {
                    echo "🔧 Building Spring Boot backend..."
                    sh 'mvn clean install -DskipTests'
                }
            }
        }

        stage('Backend - Tests') {
            steps {
                dir('inventory-back-end') {
                    echo "🧪 Running backend tests..."
                    sh 'mvn test'
                }
            }
        }

        stage('Backend - Package') {
            steps {
                dir('inventory-back-end') {
                    echo "📦 Packaging backend..."
                    sh 'mvn package'
                }
            }
        }

        /* === FRONTEND === */
        stage('Frontend - Install Dependencies') {
            steps {
                dir('inventory-front-end') {
                    echo "📦 Installing Angular dependencies..."
                    sh 'npm install'
                }
            }
        }

        stage('Frontend - Build') {
            steps {
                dir('inventory-front-end') {
                    echo "⚙️ Building Angular app..."
                    sh 'npm run build'
                }
            }
        }

        /* === ARCHIVE ARTIFACTS === */
        stage('Archive Artifacts') {
            steps {
                echo "📁 Archiving backend + frontend build outputs..."
                archiveArtifacts artifacts: 'inventory-back-end/target/*.jar', fingerprint: true
                archiveArtifacts artifacts: 'inventory-front-end/dist/**', fingerprint: true
            }
        }

    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check logs."
        }
    }
}
