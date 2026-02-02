pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/BenhurBakki/charity.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t charity-app .'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh '''
                docker stop charity charity-2 || true
                docker rm charity charity-2 || true

                docker run -d --name charity -p 8080:8080 charity-app
                docker run -d --name charity-2 -p 8081:8080 charity-app
                '''
            }
        }
    }
}
