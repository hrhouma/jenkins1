pipeline {
    agent none // Permet de spécifier que chaque étape définira son propre agent.
    stages {
        stage('Checkout code') {
            agent any // Utilise n'importe quel agent disponible pour le checkout.
            steps {
                checkout scm // Utilise la configuration SCM définie dans le projet Jenkins pour récupérer le code.
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:14-alpine' // Utilise l'image Docker spécifiée pour cette étape.
                    args '-p 3000:3000' // Arguments passés au conteneur Docker, si nécessaire.
                }
            }
            steps {
                sh 'npm install' // Exécute 'npm install' à l'intérieur du conteneur Docker.
                sh 'npm run build' // Pour une application Node.js, par exemple.
            }
        }
    }
    post {
        always {
            echo 'Nettoyage post-build...'
            // Ici, vous pouvez ajouter des étapes pour nettoyer après le build.
        }
    }
}
