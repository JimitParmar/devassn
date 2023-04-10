pipeline {
    agent {
        docker {
            image 'node:14-alpine'
            args '-u root' // This allows the container to run as root
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'npm install http-server'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'http-server ./dist -p 8080 &'
            }
        }
    }
}
