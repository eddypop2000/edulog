pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t edulog:latest .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run the tests in a Docker container
                    sh 'docker run --rm edulog:latest python -m unittest discover -s . -p "test_*.py"'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
