pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            agent {
                docker {
                    image 'docker:latest' // Use a Docker image with Docker CLI
                    args '-u root' // Run as root if needed
                }
            }
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t edulog:latest .'
                }
            }
        }

        stage('Run Tests') {
            agent {
                docker {
                    image 'docker:latest' // Use the same or another Docker image for tests
                    args '-u root'
                }
            }
            steps {
                script {
                    // Run the tests in a Docker container
                    sh 'docker run --rm edulog:latest python -m unittest discover -s . -p "test_*.py"'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Optionally clean up images
            sh 'docker rmi edulog:latest || true'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
