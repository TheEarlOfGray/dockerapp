pipeline {
    agent any
    environment {
        DOCKER_LOGIN=credentials('DOCKER_LOGIN')
    }
    stages{
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
            }
        }
        stage('Build') {
            steps {
                sh 'docker stop theearlofgray/app1'
                sh 'docker rm theearlofgray/app1'
                sh 'docker build -t theearlofgray/app1 .'
                sh 'docker login -u ${DOCKER_LOGIN_USR} -p ${DOCKER_LOGIN_PSW}'
                sh 'docker push theearlofgray/app1'
                
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 --name app1 theearlofgray/app1'
                
            }
        }
    }
}