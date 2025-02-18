pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // In a Freestyle job, the checkout is usually handled by Jenkins itself.
                // You might not even need this stage if your Freestyle job is already set up to checkout.
                // If you *do* need it, use the git step:
                git branch: 'main', url: 'https://github.com/qureshiadeel/tst.git'  // Replace with your repo URL and branch
            }
        }

        stage('Build') {
            steps {
                // If you have a build process (e.g., npm build, etc.)
                // sh 'npm install'
                // sh 'npm run build'

                // If it's just static HTML, you might not have a build step.
                echo "No build step needed for static website (if applicable)."
            }
                  }

        stage('Test') {
            steps {
                echo "Running tests..."
                echo "This is a static website - basic tests can be added here."
                // Add your tests here if needed.
            }
            post {
                failure {
                    echo "Tests failed! Stopping the pipeline."
                    currentBuild.result = 'UNSTABLE'
                }
            }
        }

       stage('Deploy') {
    when {
        expression { currentBuild.result != 'UNSTABLE' && currentBuild.result != 'FAILURE' }
    }
    steps {
        // Stop and remove existing containers (important!)
        sh 'docker-compose down -v'  // Stops and removes all containers defined in docker-compose.yml

        // Start the containers in detached mode
        sh 'docker-compose up -d --build'

        echo "Containers deployed using docker-compose up -d"
    }
}
    }
}
