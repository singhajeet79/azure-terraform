pipeline {
    agent any

    environment {
        AZURE_SUBSCRIPTION_ID = credentials('AZURE_SUBSCRIPTION_ID')
        AZURE_CLIENT_ID = credentials('AZURE_CLIENT_ID')
        AZURE_CLIENT_SECRET = credentials('AZURE_CLIENT_SECRET')
        AZURE_TENANT_ID = credentials('AZURE_TENANT_ID')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/singhajeet79/azure-terraform.git'
            }
        }
        
        stage('Terraform Init') {
            steps {
                sh """
                    terraform init
                """
            }
        }
        
        stage('Terraform Plan') {
            steps {
                sh """
                    terraform plan -var subscription_id=$AZURE_SUBSCRIPTION_ID -var client_id=$AZURE_CLIENT_ID -var client_secret=$AZURE_CLIENT_SECRET -var tenant_id=$AZURE_TENANT_ID
                """
            }
        }
        
        stage('Terraform Apply') {
            steps {
                sh """
                    terraform apply -auto-approve -var subscription_id=$AZURE_SUBSCRIPTION_ID -var client_id=$AZURE_CLIENT_ID -var client_secret=$AZURE_CLIENT_SECRET -var tenant_id=$AZURE_TENANT_ID
                """
            }
        }
    }
}
