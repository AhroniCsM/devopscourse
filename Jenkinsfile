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
                    sh 'DOCKER_BUILDKIT=1 docker build --target producer -t producer ./producer'
                    sh 'DOCKER_BUILDKIT=1 docker build --target consumer -t consumer ./consumer'

                    // Tag Docker images
                    sh "docker tag producer ${producerImage}"
                    sh "docker tag consumer ${consumerImage}"

                    // Push Docker images
                    sh "docker push ${producerImage}"
                    sh "docker push ${consumerImage}"
                }
            }
        }

        stage('Manual Deployment Approval') {
            steps {
                script {
                    // Prompt for manual approval
                    def userInput = input(
                        id: 'manual-approval',
                        message: 'Do you want to deploy?',
                        parameters: [choice(choices: ['Yes', 'No'], description: 'Select Yes to deploy', name: 'DEPLOY')]
                    )

                    // Check user input
                    if (userInput == 'No') {
                        error('Deployment aborted by user')
                    }
                }
            }
        }

        stage('Continuous Deployment') {
            steps {
                script {
                    // Load Kubernetes credentials
                    def kubeConfig = credentials('895743')

                    // Define Helm release name and namespace
                    def releaseName = 'my-release-devops-course'
                    def namespace = 'default'

                    // Add your helm chart path
                    def helmChartPath = '/Users/nanoxai/Desktop/Courses/devops_expert/devops course/devopscourse/my-umbrella-chart-0.1.0.tgz'

                    // Upgrade Helm chart using kubeconfigg
                    withCredentials([kubeconfigFile(credentialsId: '895743', variable: 'KUBECONFIG')]) {
                    sh "helm upgrade --install ${releaseName} ${helmChartPath} -n ${namespace} --set image.tag=latest"
                }
            }
        }
    }
}




