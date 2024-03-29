pipeline {
    agent any
    
    tools {
        gradle 'Gradle87'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/RinRavit/DevOps.git'
            }
        }
        stage('Build'){
            steps{
                sh 'gradle clean build'
            }
        }
        stage('Test'){
            steps{
                sh 'gradle test'
            }
        }
    }
    post{
        success {
            // Send email notification for success
            emailext (
                to: 'recipient@example.com',
                subject: 'Pipeline Success',
                body: 'Your Jenkins pipeline has completed successfully.'
            )
        }
        failure {
            // Send email notification for failure
            emailext (
                to: 'recipient@example.com',
                subject: 'Pipeline Failure',
                body: 'Your Jenkins pipeline has failed. Please check the logs for details.'
            )
        }
    }
}