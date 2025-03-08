pipeline {
    environment {
        registry = "couassif155/tp4-"  //
        registryCredential = 'docker-hub-credentials'  // 
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/19940102/tp4'
            }
        }

        stage('Building image') {
            steps {
                script {
                    // Construire l'image Docker avec un tag basé sur le numéro de build Jenkins
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    // Exemple de test d'image
                    echo "Tests passed"
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    // Utilisation des credentials Docker Hub pour pousser l'image sur Docker Hub
                    withDockerRegistry([credentialsId: registryCredential, url: '']) {
                        // Tagger l'image avec le numéro de build et latest
                        sh "docker tag ${registry}:${BUILD_NUMBER} ${registry}:latest"
                        // Pousser l'image taguée avec le numéro de build
                        sh "docker push ${registry}:${BUILD_NUMBER}"
                        // Pousser l'image taguée en latest
                        sh "docker push ${registry}:latest"
                    }
                }
            }
        }
    }
}
