# New-jenkins
pipeline {
    agent any

    environment {
        PROJECT_NAME = "New-jenkins"
        DEPLOY_DIR = "/var/www/html/${PROJECT_NAME}"
    }

    stages {
        stage('📥 Clone Code') {
            steps {
                echo "Cloning repo from GitHub..."
                git branch: 'main', url: 'https://github.com/Rajat-shamra/New-jenkins.git'
            }
        }

        stage('🔍 Check Files') {
            steps {
                echo "Listing project files..."
                sh 'ls -la'
            }
        }

        stage('🧪 Test or Validate') {
            steps {
                echo "No tests defined yet, skipping test stage..."
                // Add real test commands here if needed
            }
        }

        stage('🚀 Deploy') {
            steps {
                echo "Deploying files to local directory..."
                sh '''
                    mkdir -p ${DEPLOY_DIR}
                    cp -r * ${DEPLOY_DIR}
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}

