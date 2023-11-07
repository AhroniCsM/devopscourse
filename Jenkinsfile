properties([pipelineTriggers([pollSCM('* * * * *')])])
pipeline {
    agent any

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
    }
}
