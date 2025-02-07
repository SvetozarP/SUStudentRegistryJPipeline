pipeline {
    agent any  // Runs on any available Windows agent

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
                    bat """
                    echo Installing Node.js...
                    node -v || choco install nodejs --version=${NODE_VERSION} -y
                    node -v
                    """
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    bat 'npm install'
                }
            }
        }

        stage('Start Application') {
            steps {
                script {
                    echo 'Starting the application...'
                    bat 'start /b npm start'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                    bat 'npm test'
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