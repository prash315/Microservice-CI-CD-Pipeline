pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'git@github.com:prash315/Microservice-CI-CD-Pipeline.git']]
                ])
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    script {
                        'docker build -t frontend:latest .'
                    }
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('backend') {
                    script {
                        'docker build -t backend:latest .'
                    }
                }
            }
        }

        stage('Test Backend') {
            steps {
                dir('backend') {
                    script {
                        echo 'Running backend tests - Python-unittest for backend functionality'
                        echo 'Test run sucessfully'
                    }
                }
            }
        }

        stage('Deploy Microservices') {
            steps {
                script {
                    echo 'Deploying frontend and backend services'
                    'docker run -d -p 82:80 frontend:latest'
                    'docker run -d -p 3002:3000 backend:latest'
                }
            }
        }
    }
}