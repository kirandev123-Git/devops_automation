pipeline {
    agent {
        docker {
            image 'maven:3.8.5-openjdk-17' // Base image with Maven pre-installed
            args '-u root' // Run as root to install additional packages like npm
        }
    }

    environment {
        NODE_VERSION = '18.17.1'
    }

    stages {
        stage('Install Node.js & npm') {
            steps {
                sh '''
                    echo "Installing Node.js and npm..."
                    apt-get update
                    apt-get install -y curl

                    curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                    apt-get install -y nodejs

                    echo "Node.js version: $(node -v)"
                    echo "npm version: $(npm -v)"
                '''
            }
        }

        stage('Verify Maven') {
            steps {
                sh 'mvn -version'
            }
        }

        stage('Verify npm') {
            steps {
                sh 'npm -v'
            }
        }
    }

    post {
        always {
            echo 'Build complete.'
        }
    }
}
