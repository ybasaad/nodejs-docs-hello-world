pipeline {
    agent any
    environment {
		  DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-hk')
    }
    stages {
        stage('Clean') {
            steps {
                sh 'docker stop helloworld && docker rm helloworld'
                sh 'docker rm hamzhkoujan/hk-helloworld'
            }
        }
      stage('Build') {
            steps {
                sh 'docker build --tag helloworld:$BUILD_NUMBER .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &'
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
      stage('Tag') {
            steps {
                sh 'docker tag helloworld hamzhkoujan/hk-helloworld'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push hamzhkoujan/hk-helloworld'
            }
        }
    }
  post {
	  always {
		  sh 'docker logout'
	  }
  }
}
