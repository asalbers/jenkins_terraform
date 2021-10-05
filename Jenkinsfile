pipeline {
    agent any 
    stages {
        stage('Checkout') {
            checkout scm
        }
        stage('terraform validate') {
            steps{
                echo 'validating'
                sh (
                    returnStdout: true,
                    script: "terraform validate"
                )
            }

        }
        stage('terraform plan') {

        }
    }
}