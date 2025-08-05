pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/rushi033/hackthon213.git'
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
            mail(
                to: 'rushidon3389@gmail.com',
                subject: "✅ CI/CD Success: ${env.JOB_NAME}",
                body: "The pipeline completed successfully!"
            )
        }
        failure {
            mail(
                to: 'rushidon3389@gmail.com',
                subject: "❌ CI/CD Failed: ${env.JOB_NAME}",
                body: "Check Jenkins logs for errors."
            )
        }
    }
}
