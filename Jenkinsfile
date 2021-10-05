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
                        export ARM_CLIENT_ID=$AZURE_CLIENT_ID
                        export ARM_CLIENT_SECRET=$AZURE_CLIENT_SECRET
                        export ARM_SUBSCRIPTION_ID=$AZURE_SUBSCRIPTION_ID
                        export ARM_TENANT_ID=$AZURE_TENANT_ID
                        terraform plan
                    '''
                    // echo 'validating'
                    // sh ('terraform plan')
                }
            }
        }
    }
}