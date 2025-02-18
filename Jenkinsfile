pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/qureshiadeel/tst.git'
            }
        }

        stage('Build') {
            steps {
                echo "No build step needed for static website."
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                echo "Add your tests here if needed."
            }
        }

        stage('Deploy') {
            steps {
                dockerCompose(composeFile: 'docker-compose.yml') {
                    sh 'docker-compose down -v'
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }
}
