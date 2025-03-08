pipeline {
    agent any

    environment {
        IMAGE_NAME = "mon-image:latest"
        REGISTRY = "docker.io/mon-utilisateur"
    }

    stages {
        stage('Cloning Git') {
            steps {
                git branch: 'main', url: 'https://github.com/mon-utilisateur/TP4.git'
            }
        }

        stage('Building image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    sh 'docker run --rm $IMAGE_NAME echo "Test réussi !"'
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                        sh 'docker tag $IMAGE_NAME $REGISTRY/$IMAGE_NAME'
                        sh 'docker push $REGISTRY/$IMAGE_NAME'
                    }
                }
            }
        }
    }
}
