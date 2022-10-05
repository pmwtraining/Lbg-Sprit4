pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build') {
            steps {
                sh '''
                docker build -t java-app:latest .
                '''
            }
        }
        stage('Tear Down') {
            steps {
                sh '''
                docker rm java-app
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker run -p 80:8080 --name java-app java-app:latest
                '''
            }
        }
    }
    post {
            always {
                sh 'docker system prune'
            }
        }
}