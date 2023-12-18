pipeline {
    agent any
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }
    stages {
        stage('git checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/samsorrahman/10-Tier-MicroService-Appliction.git'
            }
        }
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.ProjectName=10-Tier -Dsonar.java.binaries=. '''
                }

            }

        }
        stage('adservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/adservice') {
                            sh 'docker build -t samsorrahman/adservice:latest .'
                            sh "docker push samsorrahman/adservice:latest"
                            sh "docker rmi samsorrahman/adservice:latest"
                        }
                    }
                }
            }
        }

        stage('cartservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/cartservice/src/') {
                            sh 'docker build -t samsorrahman/cartservice:latest .'
                            sh "docker push samsorrahman/cartservice:latest"
                            sh "docker rmi samsorrahman/cartservice:latest"
                        }
                    }
                }
            }
        }

        stage('checkoutservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/checkoutservice/') {
                            sh 'docker build -t samsorrahman/checkoutservice:latest .'
                            sh "docker push samsorrahman/checkoutservice:latest"
                            sh "docker rmi samsorrahman/checkoutservice:latest"
                        }
                    }
                }
            }
        }

        stage('currencyservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/currencyservice/') {
                            sh 'docker build -t samsorrahman/currencyservice:latest .'
                            sh "docker push samsorrahman/currencyservice:latest"
                            sh "docker rmi samsorrahman/currencyservice:latest"
                        }
                    }
                }
            }
        }

        stage('emailservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/emailservice/') {
                            sh 'docker build -t samsorrahman/emailservice:latest .'
                            sh "docker push samsorrahman/emailservice:latest"
                            sh "docker rmi samsorrahman/emailservice:latest"
                        }
                    }
                }
            }
        }

        stage('frontend'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/frontend/') {
                            sh 'docker build -t samsorrahman/frontend:latest .'
                            sh "docker push samsorrahman/frontend:latest"
                            sh "docker rmi samsorrahman/frontend:latest"
                        }
                    }
                }
            }
        }

        stage('loadgenerator'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/loadgenerator/') {
                            sh 'docker build -t samsorrahman/loadgenerator:latest .'
                            sh "docker push samsorrahman/loadgenerator:latest"
                            sh "docker rmi samsorrahman/loadgenerator:latest"
                        }
                    }
                }
            }
        }

        stage('paymentservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/paymentservice/') {
                            sh 'docker build -t samsorrahman/paymentservice:latest .'
                            sh "docker push samsorrahman/paymentservice:latest"
                            sh "docker rmi samsorrahman/paymentservice:latest"
                        }
                    }
                }
            }
        }

        stage('productcatalogservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/productcatalogservice/') {
                            sh 'docker build -t samsorrahman/productcatalogservice:latest .'
                            sh "docker push samsorrahman/productcatalogservice:latest"
                            sh "docker rmi samsorrahman/productcatalogservice:latest"
                        }
                    }
                }
            }
        }

        stage('recommendationservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/recommendationservice/') {
                            sh 'docker build -t samsorrahman/recommendationservice:latest .'
                            sh "docker push samsorrahman/recommendationservice:latest"
                            sh "docker rmi samsorrahman/recommendationservice:latest"
                        }
                    }
                }
            }
        }

        stage('shippingservice'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        dir('/var/lib/jenkins/workspace/10-Tier/src/shippingservice/') {
                            sh 'docker build -t samsorrahman/shippingservice:latest .'
                            sh "docker push samsorrahman/shippingservice:latest"
                            sh "docker rmi samsorrahman/shippingservice:latest"
                        }
                    }
                }
            }
        }

        stage('K8-Deploy'){
            steps{
                withKubeConfig(caCertificate: '', clusterName: 'my-eks2', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://EBCE08CF45C3AA5A574E126370E5D4FC.gr7.ap-south-1.eks.amazonaws.com') {
                    sh 'kubectl apply -f deployment-service.yml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'
                }
            }
        }
    }
}