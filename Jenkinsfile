pipeline {
    // Définition des options globales du pipeline
    agent any // Utilise n'importe quel agent disponible pour exécuter le pipeline
    // Pour ajouter un agent specifique décommenter la ligne suivante et supprimer celle du dessus
    /*
    agent {
        label 'nom_de_l_agent'
    }
    */

    // Stages du pipeline
    stages {
        // Stage de clonage du code depuis un référentiel Git
        stage('Clonage du Code') {
            steps {
                // Suppression du dossier précédent si existant
                deleteDir()
                // Étape de clonage du code depuis un dépôt Git
                git branch: 'main', url: 'https://github.com/fredericEducentre/messy_bootstrap.git'
                sh '''
                    last_pull_request=$(git ls-remote origin 'pull/*/head' | tail -n 1 )
                    last_number=$(echo "$last_pull_request" | grep -oE '/[0-9]+/' | tail -1 | tr -d '/' )
                    git fetch origin "pull/$last_number/head:pull_$last_number"
                    git checkout "pull_$last_number"
                '''
            }
        }
    }

    // Post-actions à exécuter après la fin du pipeline
    post {
        // Action à exécuter en cas d'échec du pipeline
        failure {
            // Exemple: Notification en cas d'échec du pipeline
            echo 'Le pipeline a échoué. Veuillez vérifier les logs pour plus d\'informations.'
        }

        // Action à exécuter en cas de succès du pipeline
        success {
            // Exemple: Notification en cas de succès du pipeline
            echo 'Le pipeline a réussi. Le déploiement a été effectué avec succès.'
        }
    }
}