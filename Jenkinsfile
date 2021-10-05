pipeline {
    agent any 
    stages {
        stage('Checkout') {
            steps{
                checkout scm
            }
        }
        // stage('az login'){
        //     steps{
        //         withCredentials([azureServicePrincipal('azure_id')]) {
        //             sh 'export TF_VAR_client_id=$AZURE_CLIENT_ID'
        //             sh 'export TF_VAR_client_secret=$AZURE_CLIENT_SECRET'
        //         }
        //     }
        // }
        stage('terraform init') {
            steps{
                echo 'validating'
                sh (
                    returnStdout: true,
                    script: "terraform init"
                )
            }

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
            steps{
                withCredentials([azureServicePrincipal('azure_id')]) {
                    sh  '''
                        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                    '''
                    echo 'validating'
                    sh ('terraform plan')
                }
            }
        }
    }
}