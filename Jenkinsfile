pipeline {
    agent {label "jenkins-slave"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-jenkins')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/theakshaywagh/docker_jenkins_ec2.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t theakshaywagh/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push theakshaywagh/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

