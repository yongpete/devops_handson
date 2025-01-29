/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                sh '''
                rm -rf ./*
                git clone https://github.com/yongpete/devops_handson.git
                cd devops_handson
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
}
