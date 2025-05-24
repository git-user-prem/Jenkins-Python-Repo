pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-python-push"
        IMAGE_TAG = "p2"
    }

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/git-user-prem/Jenkins-Python-Repo.git'  // or use local repo path
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                     docker.withRegistry('https://registry.hub.docker.com', 'git') {
                     app.push("${env.BUILD_NUMBER}")
                     app.push("latest")
                }
            }
        }
     }
         stage('List Docker Images') {
             steps {
                 sh 'docker images'
            }
        }
    }
}

