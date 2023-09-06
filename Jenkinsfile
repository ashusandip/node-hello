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
                sh "npm install sonarqube-scanner"
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
                withSonarQubeEnv(''){
                sh 'npm run sonar'
                  }
            }
        } 
        stage('Quality Gate') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error("Quality Gate did not pass: ${qg.status}")
                    }
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
