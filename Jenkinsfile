pipeline {

    agent any

    stages {
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