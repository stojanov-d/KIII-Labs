pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                script {
                    app = docker.build("stojanov-d/kiii-labs")
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-kiii') {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
