pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/qureshiadeel/tst.git'
            }
        }

        stage('Build') {  // No dist folder, so no build needed
            steps {
                echo "No build step needed for static website."
            }
            // No post block needed here since there are no artifacts to archive
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                echo "Add your tests here if needed."
               // post {
                 //   failure {
                   //     echo "Tests failed! Stopping the pipeline."
                     //   currentBuild.result = 'UNSTABLE'
                   // }
                }
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result != 'UNSTABLE' && currentBuild.result != 'FAILURE' }
            }
            steps {
                sh 'docker-compose down -v'
                sh 'docker-compose up -d --build'
                echo "Containers deployed using docker-compose up -d"
            }
        }
    }
}
