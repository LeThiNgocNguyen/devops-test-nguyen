pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token-devops-test')
    }

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
                echo 'Deploying website to Vercel...'

                sh '''
                    docker run --rm \
                        -e VERCEL_TOKEN="$VERCEL_TOKEN" \
                        -v "$PWD:/app" \
                        -w /app \
                        node:22 \
                        npx vercel --prod --yes --token="$VERCEL_TOKEN"
                '''
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESS'
            echo 'DEPLOY SUCCESS'
        }

        failure {
            echo 'BUILD FAILED OR DEPLOY FAILED'
        }
    }
}