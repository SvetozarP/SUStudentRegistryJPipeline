pipeline {
    agent any

    environment {
        NODE_VERSION = '18'  // Change to your required Node.js version
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    echo 'Checking out the code...'
                    checkout scm
                }
            }
        }

        stage('Set Up Node.js') {
            steps {
                script {
                    echo "Setting up Node.js version ${NODE_VERSION}"
                    sh "nvm install ${NODE_VERSION} || true"
                    sh "nvm use ${NODE_VERSION} || true"
                    sh "node -v"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    sh 'npm install'
                }
            }
        }

        stage('Start Application') {
            steps {
                script {
                    echo 'Starting the application...'
                    sh 'npm start &'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'npm test'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and Tests Passed Successfully!'
        }
        failure {
            echo '❌ Build or Tests Failed! Check logs.'
        }
    }
}
