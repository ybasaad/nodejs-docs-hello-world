pipeline {
    agent any
    environment {
		  DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-yousef')
    }
    stages {
        stage('Clean') {
            steps {
                sh 'docker rm -f $(docker ps -a -q) || true'
            }
        }
      stage('Build') {
            steps {
                sh 'docker build --tag yousef-helloworld:$BUILD_NUMBER .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run --name yousef-helloworld -p 1444:1337 yousef-helloworld:$BUILD_NUMBER node /var/www/index.js &'
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
      stage('Tag') {
            steps {
                sh 'docker tag yousef-helloworld:$BUILD_NUMBER ybasaad/yousef-helloworld:$BUILD_NUMBER'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push ybasaad/yousef-helloworld:$BUILD_NUMBER'
            }
        }
    }
  post {
	  always {
		  sh 'docker logout'
	  }
  }
}
