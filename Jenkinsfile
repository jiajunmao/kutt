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
                    if (env.BRANCH_NAME == 'v2-beta') {
                        sh 'docker build --tag=kutt:latest .'
                        sh 'docker tag kutt:latest registry.chinaeliteacademy.org/kutt:latest'
                        sh 'docker push registry.chinaeliteacademy.org/kutt:latest'
                    } else if (env.BRANCH_NAME == 'develop') {
                        sh 'docker build --tag=kutt:dev .'
                        sh 'docker tag kutt:dev registry.chinaeliteacademy.org/kutt:dev'
                        sh 'docker push registry.chinaeliteacademy.org/kutt:dev'
                    }
                }
            }
        }

        stage('Deployment - Docker') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'v2-beta') {
                        echo 'v2-beta detected, updating cea docker stack'
                        sh 'ssh aaronmao@mag.server.kentailab.org "cd /data/dockers/kutt && docker stack deploy --compose-file=docker-compose.yml --with-registry-auth kutt"'
                    }
                }
            }
        }
    }
}