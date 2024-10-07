pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/khalilarfaoui/jenkins-spirng-boot-bankapp.git', branch: 'main'
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

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy Locally') {
            steps {
                sh '''
                   cp target/accounts-0.0.1-SNAPSHOT.jar /opt/deployment/mon-application.jar
                   bash /opt/deployment/start.sh
                   '''
            }
        }
    }

    post {
        success {
            echo 'Déploiement réussi sur le VPS (local) !'
        }
        failure {
            echo 'Le déploiement a échoué.'
        }
    }
}
