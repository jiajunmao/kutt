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
        
        stage('Test') {
            steps {
                script {
                    sh 'yarn test'
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
    }
}