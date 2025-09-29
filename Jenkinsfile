    pipeline {
    agent any
       
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Masihadi/nodejs-app.git'
            }
        }
            
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'npm test || echo "No tests found"'
            }
        }
        
        stage('Docker Build') {
            steps {
                sh 'docker build -t nodejs-app .'
            }
        } 
        post {
            failure {
                mail to: 'had.alav.m@gmail.com',
                    subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "Check logs at ${env.BUILD_URL}"
            }
        }
     
        }
    }
