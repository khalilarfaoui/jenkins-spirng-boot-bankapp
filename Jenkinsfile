pipeline {
    agent any

    environment {
        APP_NAME = "mon-application"          // Nom de l'application
        DEPLOY_DIR = "/opt/deployment"        // Dossier de déploiement sur le serveur local
        JAR_FILE = "mon-application.jar"      // Nom du fichier JAR après construction
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/khalilarfaoui/jenkins-spirng-boot-bankapp.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Construction du projet avec Maven
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Exécution des tests Maven
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Construction du fichier JAR
                sh 'mvn package'
            }
        }

        stage('Deploy Locally') {
            steps {
                // Déploiement local : Copier le fichier JAR dans le répertoire de déploiement
                sh """
                echo "Copie du fichier JAR dans le répertoire de déploiement..."
                cp target/$JAR_FILE $DEPLOY_DIR/
                """
            }
        }

        stage('Restart Application') {
            steps {
                // Redémarrer l'application sur le serveur local
                sh """
                echo "Arrêt des anciennes instances..."
                pkill -f 'java -jar' || true  # Ignorer les erreurs si aucune instance n'est en cours d'exécution

                echo "Démarrage de la nouvelle instance..."
                nohup java -jar $DEPLOY_DIR/$JAR_FILE > $DEPLOY_DIR/app.log 2>&1 &
                echo "Application démarrée !"
                """
            }
        }
    }

    post {
        success {
            echo 'Déploiement local réussi !'
        }
        failure {
            echo 'Le pipeline a échoué.'
        }
    }
}
