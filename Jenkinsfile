pipeline {
    agent any
    environment {
        GIT_Info = str(script: "git describe --tags --exact-match || echo 'no_tag'", returnStdout: true).trim()
    }

    stages {
        stage("Verificar Tag") {
            steps {
                script {
                    if (env.GIT_Info != "no_tag") {
                        echo "Este commit foi disparado por uma tag: ${env.GIT_Info}"
                    } else {
                        echo "Este commit não é uma tag. Nenhuma ação especial será executada."
                    }
                }
            }
        }

        stage("Build Release") {
            when {
                expression { env.GIT_Info != "no_tag" }
            }
            steps {
                echo "Executando build de release para versão ${env.GIT_Info}"
            }
        }
    }

    post {
        always {
            echo "Build finalizado."
        }
    }
}
