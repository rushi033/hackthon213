pipeline {
    agent { label 'docker-agent' }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/rushi033/hackthon213.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Test') {
            steps {
                sh 'curl -f http://localhost:5000 || exit 1'
            }
        }
    }

    post {
        success {
            mail to: 'rushi033@example.com',
                 subject: "✅ CI/CD Success: ${env.JOB_NAME}",
                 body: "The pipeline completed successfully!"
        }
        failure {
            mail to: 'rushi033@example.com',
                 subject: "❌ CI/CD Failed: ${env.JOB_NAME}",
                 body: "Check Jenkins logs for errors."
        }
    }
}

