pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodejs-app .'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'docker rm -f nodejs-app || true'
                sh 'docker run -d -p 3000:3000 --name nodejs-app nodejs-app'
            }
        }
    }

    post {
        failure {
            mail to: 'had.alav.m@gmail.com',
                 subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Something went wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}\nCheck logs at: ${env.BUILD_URL}"
        }
    }
}
