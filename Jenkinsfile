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
               // }
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result != 'UNSTABLE' && currentBuild.result != 'FAILURE' }
            }
             steps {
        withDockerCompose(composeFile: 'docker-compose.yml') { // Make sure the path is correct if docker-compose.yml is not at the root of the workspace
            sh 'docker-compose down -v' // or dockerCompose('down', '-v')
            sh 'docker-compose up -d --build' // or dockerCompose('up', '-d', '--build')
            echo "Containers deployed using docker-compose up -d"

        }
    }
         //   steps {
           //     sh 'docker-compose down -v'
             //   sh 'docker-compose up -d --build'
               // echo "Containers deployed using docker-compose up -d"
            //}
        }
    }
}
