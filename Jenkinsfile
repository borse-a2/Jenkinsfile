pipeline {
    agent any

    environment {
        ARM_CLIENT_ID       = credentials('69fa969d-48d1-445c-9f48-fbae54f12da7')
        ARM_CLIENT_SECRET   = credentials('i158Q~10YymEF7smvptXb.xhYbxRWzuNgBD8KacT')
        ARM_SUBSCRIPTION_ID = credentials('acd6d659-39c8-4397-9cb1-fe8ece5fbbfb')
        ARM_TENANT_ID       = credentials('c4986e28-914d-448c-96c8-e4e078b8384e')
    }

    stages {
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan || exit 1'
            }
        }

        stage('Terraform Apply') {
            steps {
                input message: 'Approve deployment?'
                sh 'terraform apply tfplan || exit 1'
            }
        }
    }

    post {
        success {
            echo '✅ Terraform deployment completed successfully.'
        }
        failure {
            echo '❌ Terraform deployment failed.'
        }
    }
}

