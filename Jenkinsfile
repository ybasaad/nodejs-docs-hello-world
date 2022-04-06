pipeline {
    agent any
    stages {
        stage('Clean') {
            steps {
                sh 'docker stop yousef-helloworld && docker rm yousef-helloworld || true'
            }
        }
      stage('Build') {
            steps {
                sh 'docker build --tag yousef-helloworld:$BUILD_NUMBER .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run --name yousef-helloworld -p 11444:1337 yousef-helloworld:$BUILD_NUMBER node /var/www/index.js &'
            }
        }
        
    }
}
