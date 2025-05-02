pipeline {
    agent any

    environment {
        IS_TAG = "false"
    }

    stages {
        stage('Checar se é uma tag') {
            steps {
                script {
                    // Verifica se estamos construindo uma tag
                    if (env.GIT_TAG_NAME) {
                        echo "Este é um build de TAG: ${env.GIT_TAG_NAME}"
                        env.IS_TAG = "true"
                    } else {
                        echo "Este não é um build de tag."
                    }
                }
            }
        }

        stage('Build normal') {
            when {
                expression { return env.IS_TAG == "false" }
            }
            steps {
                echo "Executando build comum (sem tag)"
            }
        }

        stage('Build de release (com tag)') {
            when {
                expression { return env.IS_TAG == "true" }
            }
            steps {
                echo "Executando ação especial para TAG (ex: deploy, build de release)"
            }
        }
    }
}