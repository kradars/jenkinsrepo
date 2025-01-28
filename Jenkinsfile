pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('accesskey')  // Use the Jenkins credential ID
        AWS_SECRET_ACCESS_KEY = credentials('secretkey')  // Use the Jenkins credential ID
        AWS_REGION = 'ap-south-1'  // Replace with your AWS region
        EB_APP_NAME = 'JavaApp'  // Your Elastic Beanstalk Application Name
        EB_ENV_NAME = 'JavaApp-env'  // Your Elastic Beanstalk Environment Name
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
                    // Build your Java application using Maven
                    sh 'mvn clean install'
                }
            }
        }
        stage('Deploy to Elastic Beanstalk') {
            steps {
                script {
                    // Initialize Elastic Beanstalk CLI for your application
                    sh '''
                        eb init $EB_APP_NAME --region $AWS_REGION --platform "java" --no-verify-ssl
                    '''
                    // Deploy the Java application to Elastic Beanstalk
                    sh '''
                        eb deploy $EB_ENV_NAME --region $AWS_REGION
                    '''
                }
            }
        }
    }
}
