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

        stage('Build') {
            steps {
                script {
                    sh 'yarn build'
                }
            }
        }

        stage('Deployment - Git') {
            steps {
                script {
                    sh 'ssh aaronmao@thinkpad.kentailab.org "cd /myssddisk/dockers/kutt && git pull"'
                }
            }
        } 

        stage('Deployment - Docker') {
            steps {
                script {
                    sh 'ssh aaronmao@thinkpad.kentailab.org "cd /myssddisk/dockers/kutt && docker-compose restart"'
                }
            }
        }
    }
}