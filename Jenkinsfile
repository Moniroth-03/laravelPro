pipeline {
    agent any // window agent, Jenkins-laravel (other machine)

    stages {
        stage('Fetch from GitHub') { //build steps
            steps {
                echo 'Fetching for GitHub'
                git branch: 'main' , url: 'https://github.com/Moniroth-03/laravelPro.git'
            }
        }
        stage('Composer install') {
            steps {
                sh 'composer install'
            }
        }
        stage('Copy .env') {
            steps {
                sh 'cp .env.example .env'
            }
        }
        stage('Add key') {
            steps {
                echo 'running code ...'
                sh 'php artisan key:generate'
            }
        }
        stage('npm') {
            steps {
                echo 'Compiling code ...'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test the app'){
            steps{
                echo 'Testing unit tests...'
                echo 'Testing feature...'
                sh 'php artisan test'
            }
        }
    }

    post {
        // success {
        //     sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"1160695842\", \"text\": \"[SUCCESS] Ukata api build success!\", \"disable_notification\": false}\' https://api.telegram.org/bot6751032720:AAFdUFPbsOShMqa6njLDAF6inRD380ZyHAo/sendMessage'
        // }
        failure {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"1160695842\", \"text\": \"[FAILED] Ukata api build failed!\", \"disable_notification\": false}\' https://api.telegram.org/bot6751032720:AAFdUFPbsOShMqa6njLDAF6inRD380ZyHAo/sendMessage'
        }
    }
}
