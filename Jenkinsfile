pipeline {
    agent any
    tools {
        maven 'Maven3'  // Defined in Jenkins global tools config
        jdk 'JDK11'     // Make sure JDK11 is installed in Jenkins
    }
    environment {
        SONAR_HOST_URL = 'http://your-sonarqube-server'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-org/my-devops-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Deploy Artifact') {
            steps {
                sh 'mvn deploy'
            }
        }
    }
    post {
        success {
            echo 'Build and deploy successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
