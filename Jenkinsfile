// properties([pipelineTriggers([pollSCM('* * * * *')])])
pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('Checkout') {
            steps {
                git 'https://github.com/AhroniCsM/devopscourse.git'
            }
        }
        stage('Build and Push Docker images') {
            steps {
                script {
                    def dockerImage = 'aharoniscsm/producer:latest'
                    
                    // Build Docker image
                    sh 'docker build -t producer ./producer'
                    sh 'docker build -t consumer ./consumer'
                    
                    // Tag Docker image
                    sh "docker tag producer ${dockerImage}"
                    sh "docker tag consumer ${dockerImage}"
                    
                    // Push Docker image
                    sh "docker push ${dockerImage}"
                    sh "docker push ${dockerImage}"
                }
            }
        }
    }
}