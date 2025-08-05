pipeline {
    agent { label 'docker-agent' }

    environment {
        COMPOSE_PROJECT_NAME = 'flaskapp'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/flask-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Deploy App') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Health Check') {
            steps {
                sh 'sleep 5' // give it time to boot
                sh 'curl -f http://localhost:5000 || exit 1'
            }
        }
    }

    post {
        success {
            mail to: 'your-email@example.com',
                 subject: "✅ Jenkins CI/CD Success",
                 body: "The Flask app was built and deployed successfully."
        }

        failure {
            mail to: 'your-email@example.com',
                 subject: "❌ Jenkins CI/CD Failed",
                 body: "Check the Jenkins logs for errors."
        }
    }
}
