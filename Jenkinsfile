pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('accesskey')  // Use credentials stored in Jenkins
        AWS_SECRET_ACCESS_KEY = credentials('secretkey')
        AWS_REGION = 'ap-south-1'  // Replace with your region
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kradars/jenkinsrepo.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean install'
                }
            }
        }
        stage('Deploy to Elastic Beanstalk') {
            steps {
                script {
                    sh '''
                        eb init -p java --region $AWS_REGION
                        eb deploy
                    '''
                }
            }
        }
    }
}
