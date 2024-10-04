pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mon-utilisateur/mon-projet.git', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Exécute le build Maven
                    sh 'mvn clean install'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Exécute les tests Maven
                    sh 'mvn test'
                }
            }
        }
        
        stage('Package') {
            steps {
                script {
                    // Emballe l'application en JAR/WAR
                    sh 'mvn package'
                }
            }
        }
        
       
    }
}
