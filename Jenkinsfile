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
                        dockerImage = docker.build registry + ":${env.BUILD_NUMBER}"
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
             sh "docker rmi $registry:${env.BUILD_NUMBER}"
          }
        }
    }
}
