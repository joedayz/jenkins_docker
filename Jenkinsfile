pipeline {
    environment {
        IMAGEN = "joedayz/myjoedayzapp"
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
                    def dockerClient = tool name: 'docker', type: 'hudson.plugins.tool.DockerTool'
                    env.PATH = "${dockerClient}/bin:${env.PATH}"
                    def newApp = docker.build("${IMAGEN}:${BUILD_NUMBER}")
                }
            }
        }
    }
}
