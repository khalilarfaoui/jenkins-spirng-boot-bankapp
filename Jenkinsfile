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
                   echo "Copie du fichier JAR dans le dossier de déploiement..."
                   cp target/accounts-0.0.1-SNAPSHOT.jar /opt/deployment/mon-application.jar
                   '''
            }
        }

        stage('Restart Application') {
            steps {
                sh '''
                   echo "Arrêt de l'application en cours..."
                   pkill -f 'java -jar' || echo "Pas d'application en cours"
                   
                   echo "Démarrage de la nouvelle version..."
                   bash /opt/deployment/start.sh
                   echo "Application démarrée avec succès !"
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
