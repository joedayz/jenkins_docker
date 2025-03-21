pipeline {
    environment {
        IMAGEN = "joedayz/demodevsecops"
        USUARIO = 'USER_DOCKERHUB'
    }
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: "main", url: 'https://github.com/joedayz/jenkins_docker.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    newApp = docker.build "$IMAGEN:$BUILD_NUMBER"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    bat  "docker run --rm --entrypoint apache2ctl $IMAGEN:$BUILD_NUMBER -v"
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry( '', USUARIO ) {
                        newApp.push()
                    }
                }
            }
        }
        stage('Clean Up') {
            steps {
                bat "docker rmi $IMAGEN:$BUILD_NUMBER"
                }
        }
    }
}
