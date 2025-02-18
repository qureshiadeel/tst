pipeline {
    agent any

    stages {
      
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
                    sh 'docker compose down -v'
                    sh 'docker compose up -d --build'
                }
            }
        }
    }
}
