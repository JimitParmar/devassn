pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                checkout scm
            }
        }
        
        stage('Build and Test') {
            steps {
                // Install dependencies and run tests for NodeJS application
                sh 'cd node-app && npm install'
                sh 'cd node-app && npm test'
                
                // Build and test PHP application
                sh 'cd php-app && composer install'
                sh 'cd php-app && phpunit'
                
                // Build HTML application
                sh 'cd html-app && npm install'
                
                // Build Flask application
                sh 'cd flask-app && pip install -r requirements.txt'
                sh 'cd flask-app && pytest'
            }
        }
        
        stage('Deploy to NodeJS container') {
            when {
                branch 'master'
            }
            steps {
                // Deploy NodeJS application to container
                sh 'cd node-app && npm run build'
                // Copy build artifacts to container
                sh 'scp -r node-app/dist/* user@node-container:/var/www/node-app/'
            }
        }
        
        stage('Deploy to Tomcat container') {
            when {
                branch 'develop'
            }
            steps {
                // Build WAR file for Java web application
                sh 'cd java-app && mvn clean package'
                // Copy WAR file to Tomcat container
                sh 'scp java-app/target/*.war user@tomcat-container:/var/lib/tomcat/webapps/'
            }
        }
        
        stage('Deploy to Flask container') {
            when {
                branch 'feature/flask'
            }
            steps {
                // Deploy Flask application to container
                sh 'cd flask-app && flask build'
                // Copy build artifacts to container
                sh 'scp -r flask-app/build/* user@flask-container:/var/www/flask-app/'
            }
        }
    }
}
