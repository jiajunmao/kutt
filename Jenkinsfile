pipeline {

    agent any

    stages {
        stage('Npm Install') {
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

        stage('Docker Build') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'v2-beta') {
                        sh 'docker build --tag=kutt:latest .'
                        sh 'docker tag kutt:latest registry.chinaeliteacademy.org/kutt:latest'
                        sh 'docker login --username=$DOCKER_USRNAME --password=$DOCKER_PASSWD registry.chinaeliteacademy.org'
                        sh 'docker push registry.chinaeliteacademy.org/kutt:latest'
                    } else if (env.BRANCH_NAME == 'develop') {
                        sh 'docker build --tag=kutt:dev .'
                        sh 'docker tag kutt:dev registry.chinaeliteacademy.org/kutt:dev'
                        sh 'docker login --username=$DOCKER_USRNAME --password=$DOCKER_PASSWD registry.chinaeliteacademy.org'
                        sh 'docker push registry.chinaeliteacademy.org/kutt:dev'
                    }
                }
            }
        }

        stage('Docker Deploy') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'v2-beta') {
                        echo 'v2-beta detected, updating cea docker stack'
                        sh 'ssh aaronmao@mag.server.kentailab.org "cd /data/dockers/apps/kutt && docker stack deploy --compose-file=docker-compose.yml --with-registry-auth kutt"'
                    }
                }
            }
        }
    }
}