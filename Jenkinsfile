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
        stage('Build and Push Docker producer') {
            steps {
                script {
                    def dockerImage = 'aharoniscsm/producer:latest'
                    
                    // Build Docker image
                    sh 'docker build -t producer ./producer'
                    
                    // Tag Docker image
                    sh "docker tag producer ${dockerImage}"
                    
                    // Push Docker image
                    sh "docker push ${dockerImage}"
                }
            }
        }
    }
}