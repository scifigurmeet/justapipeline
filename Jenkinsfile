pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'us-west-2' // Replace with your AWS region
        AWS_CREDENTIALS = credentials('8c97472c-381f-4e1a-9ee6-3e8526d15888	') // Replace with your Jenkins credentials ID
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Deploy to AWS') {
            steps {
                script {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'your-aws-credentials-id']]) {
                        sh '''
                            aws deploy create-deployment \
                                --application-name web-app \
                                --deployment-group-name web-deployment-group \
                                --github-location repository=scifigurmeet/justapipeline,commitId=${GIT_COMMIT}
                        '''
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
