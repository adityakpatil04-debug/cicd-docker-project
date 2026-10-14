
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code retrieved from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-demo:latest .'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                    docker rm -f cicd-demo-cicd || true
                    docker run -d --name cicd-demo-cicd -p 8082:80 --restart unless-stopped cicd-demo:latest
                '''
            }
        }

        stage('Test Website') {
            steps {
                sh '''
                    sleep 3
                    curl --fail --silent --show-error http://localhost:8082/ > /dev/null
                    echo "Website test passed!"
                '''
            }
        }
    }
}
