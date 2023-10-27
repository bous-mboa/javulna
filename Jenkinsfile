pipeline {
    agent any
    environment {
        GITHUB_USERNAME = 'bous-mboa'
        GITHUB_TOKEN = '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'
    }
    stages {
        stage('Checkout Source') {
            steps {
                script {
                    // Récupère les informations d'authentification du contexte d'environnement
                    def gitUsername = env.GITHUB_USERNAME
                    def gitToken = env.GITHUB_TOKEN

                    // Clonez le dépôt en utilisant les informations d'identification
                    git credentialsId: '', url: "https://${gitUsername}:${gitToken}@github.com/bous-mboa/sample-app.git"
                }
            }
        }
        stage ('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn install'
            }
        }
        stage ('docker build') {
            steps {
                sh 'docker build -t javulna-0.1 .'
            }
        }
        stage ('docker run container') {
            steps {
                sh 'docker stop app || true'
                sh 'docker rm app || true'
                sh 'docker run --name app -it -d -p 9000:8080 javulna-0.1'
            }
        }
    }
}
