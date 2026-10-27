pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate Docker Files') {
            steps {
                sh '''
                    test -f docker/Dockerfile
                    test -f docker/docker-compose.yml
                    test -f docker/index.html
                    echo "Docker project files validated"
                '''
            }
        }

        stage('Test Application') {
            steps {
                sh '''
                    curl --fail --silent --show-error \
                      http://localhost:8083/ \
                      -o /dev/null
                    echo "NGINX application test passed"
                '''
            }
        }
    }

    post {
        success {
            echo 'DevOps pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
