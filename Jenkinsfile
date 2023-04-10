pipeline {
	    agent any
	    
	    stages {
	        stage('Build') {
	            steps {
	                sh 'sudo npm install -g http-server'
	                timeout(time: 60, unit: 'SECONDS') {
	                    sh 'http-server &'
	                }
	            }
	        }
	        
	        stage('Stop') {
	            steps {
	                sh 'kill $(lsof -t -i:8080)'
	            }
	        }
	    }
	}
