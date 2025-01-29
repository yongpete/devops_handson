/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
        stage('Navigate') {
            steps {
                sh '''
                rm -rf ./*
                git clone https://github.com/yongpete/devops_handson.git
                cd devops_handson
                '''
            }
        }

        stage('Docker-compose') {
            steps {
                sh '''
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
}
