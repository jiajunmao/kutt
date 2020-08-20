pipeline {

    agent any

    stages {
        stage ('Prepare') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Yarn Build') {
            steps {
                script {
                    sh 'yarn build'
                }
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    sh 'docker build --tag=kutt:latest .'
                    sh 'docker tag kutt:latest registry.chinaeliteacademy.org/kutt:latest'
                    sh 'docker push registry.chinaeliteacademy.org/kutt:latest'
                }
            }
        }

        stage('Deployment - Docker') {
            steps {
                script {
                    sh 'ssh aaronmao@mag.server.kentailab.org "cd /data/dockers/kutt && docker stack deploy --compose-file=docker-compose.yml --with-registry-auth kutt"'
                }
            }
        }
    }
}