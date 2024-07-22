pipeline {
    agent any
     parameters {
        choice(name: 'AWS_CREDENTIAL_ID', choices: ['lambda-dev', 'lambda-sit'], description: 'Select the AWS credential to use')
    }
    environment {
        AWS_DEFAULT_REGION = 'eu-west-1'  // Replace with your AWS region
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Typically used to checkout source code from a version control system like Git
                // Example: git 'https://github.com/your-repo.git'
                echo 'Checking out source code...'
            }
        }
        

        
        stage('Deploy') {
            steps {
                  script {
                    // Retrieve the selected AWS credential ID from the parameter
                    def awsCredentialId = params.AWS_CREDENTIAL_ID
                // Deploy Lambda function using AWS CLI
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: awsCredentialId, secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    // Upload Lambda deployment package to S3
                    sh "aws ec2 describe-instances"
                    
                 
                } }
            }
        }
    }
    
    post {
        success {
            echo 'Lambda deployment pipeline succeeded.'
        }
        failure {
            echo 'Lambda deployment pipeline failed.'
        }
    }
}
