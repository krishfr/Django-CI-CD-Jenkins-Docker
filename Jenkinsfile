pipeline {
    agent {label 'krish'}
    stages {
        stage('code') {
            steps {
                echo 'cloning the code'
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
                echo 'Cloning successfull.'
            }
        }
        stage('build') {
            steps {
                sh 'git clean -fdx'
                echo 'build the code'
                sh 'docker build -t django-notes-app:latest .'
                echo 'Image build successfull.'
            }
        }
        stage('Pushing the image to DockerHub') {
            steps {
                  withCredentials([usernamePassword(
                    credentialsId:"dockerhubcred",
                    usernameVariable:"dockerhubuser", 
                    passwordVariable:"dockerhubpass")]){
                echo 'pushing the image to DockerHub'
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                sh "docker image tag django-notes-app:latest ${env.dockerhubuser}/django-notes-app:latest"
                sh "docker push ${env.dockerhubuser}/django-notes-app:latest"
            }
            }
        }
        stage('deploy') {
            steps {
               echo 'deploy the image'
               sh 'docker compose up -d'
            }
        }
    }
}