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
    }
}