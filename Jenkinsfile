pipeline {
    agent any

    environment {
        // On donne un nom différent pour ne pas écraser vos images locales
        SERVER_IMAGE = 'mern-server-jenkins'
        CLIENT_IMAGE = 'mern-client-jenkins'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code source...'
                // Jenkins récupère automatiquement le code du dépôt Git
            }
        }

        stage('Build - Server') {
            steps {
                echo 'Construction de l\'image Docker du Serveur...'
                sh 'docker build -t $SERVER_IMAGE ./server'
            }
        }

        stage('Build - Client') {
            steps {
                echo 'Construction de l\'image Docker du Client...'
                sh 'docker build -t $CLIENT_IMAGE ./client'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Exécution des tests (si présents)...'
                // Exemple : sh 'cd server && npm test'
            }
        }

        stage('Deploy / Run') {
            steps {
                echo 'Déploiement avec Docker Compose...'
                // On lance docker compose en arrière-plan (-d)
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline terminé avec succès ! L\'application est en ligne.'
        }
        failure {
            echo '❌ Le pipeline a échoué. Vérifiez les logs.'
        }
    }
}
