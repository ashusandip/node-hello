pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                 git branch: 'master',url: 'https://github.com/ashusandip/node-hello.git'
            }
        }
        stage('Build'){
            steps {
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
                    withSonarQubeEnv('sonarqubescanner') {
      				sh "/usr/bin/npm install verify sonar:sonar -Dsonar.projectKey=nodejspipeline-project -Dsonar.projectName='nodejspipeline project'"
    				}      
                  }
        } 
        
        stage('RunNodeJsApp') {
            steps {
                sh 'npm start'
            } 
        }
    }
   
}
