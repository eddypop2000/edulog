pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-u root'  // or any necessary arguments
        }
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t edulog:latest .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'docker run --rm edulog:latest python -m unittest discover -s . -p "test_*.py"'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
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
