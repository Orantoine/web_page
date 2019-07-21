pipeline {
    agent any
    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    environment {
        registry = "orantoine/front-docker"
        registryCredential = 'dockerhub'
    }
    stages {
        stage('Build'){
            steps{
                script {
                        dockerImage = docker.build registry + ":latest"
                }
            }
        }
        stage('Deploy Image') {
          steps{
            script {
              docker.withRegistry( '', registryCredential ) {
                dockerImage.push()
              }
            }
          }
        }
        stage('Remove Unused docker image') {
          steps{
             sh "docker rmi $registry:latest"
          }
        }
    }
}
