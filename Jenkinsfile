pipeline {
    agent any
    environment {
        PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Start') {
            
            when {
                anyOf {
                    branch 'main'
                    expression { env.GIT_BRANCH == 'origin/main' }
                }
            }
            steps {
                sh 'npm start'
            }
        }
    }

    post {
        success {
            echo 'Pipeline 성공적으로 완료!'
        }
        failure {
            echo 'Pipeline 실패!'
        }
    }
}
