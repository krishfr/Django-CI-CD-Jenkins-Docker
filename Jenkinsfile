@Library('Shared') _
pipeline {
    agent {label 'krish'}
    stages {
        stage('Hello') {
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps{
                script{
                    clone("https://github.com/LondheShubham153/django-notes-app.git","main")
                }
            }
        }
        stage('build'){
            steps{
                script{
                    build('django-notes-app','latest','krc56')
                }
            }
        }
        stage('push to DockerHub') {
            steps{
                script{
                    docker_push('django-notes-app','latest','krc56')
                }
            }
        }
        stage('Deploy') {
            steps{
                script{
                    docker_compose()
                    echo 'Finish the process...'
                }
            }
        }
    }
              
}
