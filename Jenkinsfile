/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
        stage('Navigate') {
            steps {
                sh '''
                rm -rf ./*
                git clone https://github.com/yongpete/devops_handson.git
                '''
            }
        }

        stage('Docker-compose') {
            steps {
                sh '''
                cd devops_handson
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
}
