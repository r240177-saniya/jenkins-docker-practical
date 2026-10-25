
pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
       
    stage('Check Docker') {
        steps {
            bat '"C:\\Users\\saniy\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" --version'
            bat '"C:\\Users\\saniy\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" ps'
        }
}


        stage('Build') {
            steps {
                bat 'docker build -t jenkins-web-app .'
            }
        }
        
        stage('Test') {
            steps {
                bat 'docker image inspect jenkins-web-app'
            }
        }

        stage('Deploy using Docker') {
            steps {
                bat '''
                docker rm -f jenkins-web-container 2>NUL
                docker run -d --name jenkins-web-container -p 8082:80 jenkins-web-app
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
