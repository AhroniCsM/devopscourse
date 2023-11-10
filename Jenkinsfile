pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Start your first jenkins project!'
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
                    def producerImage = 'aharoniscsm/producer:latest'
                    def consumerImage = 'aharoniscsm/consumer:latest'

                    // Build Docker images
                    sh 'docker build --build-arg CACHE_DATE=$(date) -t producer ./producer'
                    // sh 'docker build -t producer ./producer'
                    sh 'docker build -t consumer ./consumer'

                    // Tag Docker images
                    sh "docker tag producer ${producerImage}"
                    sh "docker tag consumer ${consumerImage}"

                    // Push Docker images
                    sh "docker push ${producerImage}"
                    sh "docker push ${consumerImage}"
                }
            }
        }

        // stage('Manual Deployment Approval') {
        //     steps {
        //         script {
        //             // Prompt for manual approval
        //             def userInput = input(
        //                 id: 'manual-approval',
        //                 message: 'Do you want to deploy?',
        //                 parameters: [choice(choices: ['Yes', 'No'], description: 'Select Yes to deploy', name: 'DEPLOY')]
        //             )

        //             // Check user input
        //             if (userInput == 'No') {
        //                 error('Deployment aborted by user')
        //             }
        //         }
        //     }
        // }

        stage('Continuous Deployment') {
            steps {
                script {

                    // Define Helm release name and namespace
                    def releaseName = 'aharon'
                    def namespace = 'default'
                    sh "helm package helm-chart"
                    // Add your helm chart path
                    def helmChartPath = 'my-umbrella-chart-0.1.0.tgz'
                    sh "helm upgrade --install ${releaseName} ${helmChartPath} --kube-context minikube"
                }
            }
        }
    }
}




