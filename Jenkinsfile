pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'TP03', url:'https://github.com/Chharng-Chhit/testJenkins.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
        // stage('Notification') {
        //     steps {
        //         mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Jenkins Notification', to: 'chhit085@gmail.com'
        //     }
        // }
    }
    post {
        success {
            mail(
                subject: "Pipeline Successful",
                body: "Hello,\n\nYour Jenkins pipeline has succeeded.\n\nHere are some details:\n\n- Build Number: ${env.BUILD_NUMBER}\n- Project Name: ${env.JOB_NAME}\n- Build URL: ${env.BUILD_URL}\n\n${currentBuild.currentResult}: ${currentBuild.description ?: 'No additional information available.'}\n\nRegards,\nJenkins",
                to: "chhit085@gmail.com"
            )
        }
        failure {
            mail(
                subject: "Pipeline Failed",
                body: "Hello,\n\nYour Jenkins pipeline has failed.\n\nHere are some details:\n\n- Build Number: ${env.BUILD_NUMBER}\n- Project Name: ${env.JOB_NAME}\n- Build URL: ${env.BUILD_URL}\n\n${currentBuild.currentResult}: ${currentBuild.description ?: 'No additional information available.'}\n\nRegards,\nJenkins",
                to: "chhit085@gmail.com"
            )
        }
    }
}
