pipeline {
    agent any

    stages {
        stage('Checar se é uma tag') {
            steps {
                script {
                    def isTag = env.GIT_TAG_NAME ? true : false

                    if (isTag) {
                        echo "Este é um build de TAG: ${env.GIT_TAG_NAME}"
                        // Executar lógica de release aqui se quiser
                    } else {
                        echo "Este não é um build de tag."
                    }

                    // Aqui, você pode usar `isTag` para decidir o que executar
                    // ou separar os estágios abaixo como vou mostrar
                }
            }
        }

        stage('Build normal') {
            when {
                expression { return !env.GIT_TAG_NAME }
            }
            steps {
                echo "Executando build comum (sem tag)"
            }
        }

        stage('Build de release (com tag)') {
            when {
                expression { return env.GIT_TAG_NAME }
            }
            steps {
                echo "Executando ação especial para TAG (ex: deploy, build de release)"
            }
        }
    }
}
