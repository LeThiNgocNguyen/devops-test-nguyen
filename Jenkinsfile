pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                echo 'Installing dependencies...'
                echo 'Static website - no dependencies required.'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'test -f index.html'
                sh 'test -f style.css'
                sh 'test -f app.js'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage will be configured next.'
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESS'
        }

        failure {
            echo 'BUILD FAILED'
        }
    }
}