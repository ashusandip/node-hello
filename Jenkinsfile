pipeline {
    agent any

    stages {
        stage('checkoutcode') {
            steps {
                git branch: 'master',url: 'https://github.com/ashusandip/nodejs-app-mss.git'
            }
        }
        stage('Build'){
            steps {
                sh "npm config fix"
                sh "npm install"  
            }
        }
        stage('Install and Verify Apache') {
            steps {
                sh 'apt-get update'
                        sh 'apt-get update -y && apt-get install -y apache2'
                        sh 'service apache2 start'
                        sh 'service apache2 status' // Check if Apache2 is running
                 }
        }
        stage('ExecuteSonarQubeReport') {
            steps {
                    
                        sh 'npm run sonar'
                    
                 }
        } 
        
        stage('RunNodeJsApp') {
            steps {
                sh 'chmod 777 ./scripts/runApp.sh'
                sh './scripts/runApp.sh'
            } 
        }
    }
   
}
