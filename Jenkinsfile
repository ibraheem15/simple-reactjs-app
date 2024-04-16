pipeline {

    agent any

    tools {
        nodejs 'Node'
    }
    
    stages {
        stage('Checkout') {
            steps {
                sh 'git clone https://github.com/ibraheem15/simple-reactjs-app.git'
            }
        }
        stage('build') {
          steps {
              sh 'npm install'
            }
        }            
        stage('Install Docker') {
            steps {
                script {
                    def dockerHome = tool 'Docker'
                    env.PATH = "/usr/bin/docker"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t simple-reactjs-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 3000:3000 simple-reactjs-app'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub', variable: 'DOCKERHUB')]) {
                    sh 'docker login -u ibraheem15 -p $DOCKERHUB'
                    sh 'docker tag simple-reactjs-app ibraheem15/simple-reactjs-app'
                    sh 'docker push ibraheem15/simple-reactjs-app'
                }
            }
        }
    }
}