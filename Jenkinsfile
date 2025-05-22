pipeline {
    agent {
        docker {
            image 'ubuntu:22.04'
            args '-u root' // Run as root to install packages
        }
    }

    environment {
        MAVEN_VERSION = '3.9.6'
        NODE_VERSION = '18.x'
    }

    stages {
        stage('Install Prerequisites') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y curl wget gnupg2 software-properties-common unzip
                '''
            }
        }

        stage('Install Maven') {
            steps {
                sh '''
                    echo "Installing Maven ${MAVEN_VERSION}..."
                    wget https://downloads.apache.org/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz
                    tar -xzf apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /opt
                    ln -s /opt/apache-maven-${MAVEN_VERSION}/bin/mvn /usr/bin/mvn
                    mvn -v
                '''
            }
        }

        stage('Install Node.js and npm') {
            steps {
                sh '''
                    echo "Installing Node.js ${NODE_VERSION}..."
                    curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION} | bash -
                    apt-get install -y nodejs
                    node -v
                    npm -v
                '''
            }
        }

        stage('Verify Tools') {
            steps {
                sh '''
                    echo "Verifying installations..."
                    mvn -v
                    node -v
                    npm -v
                '''
            }
        }
    }

    post {
        always {
            echo 'Build complete.'
        }
    }
}
