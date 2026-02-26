pipeline {
    agent any

    stages {
        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Backends') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app
                '''
            }
        }

        stage('Build Nginx') {
            steps {
                sh 'docker build -t nginx-lb nginx'
            }
        }

        stage('Run Nginx') {
            steps {
                sh '''
                docker rm -f nginx-lb || true
                docker run -d -p 80:80 --name nginx-lb nginx-lb
                '''
            }
        }
    }
}
