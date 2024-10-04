pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/khalilarfaoui/jenkins-spirng-boot-bankapp.git'  // URL de votre projet
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
