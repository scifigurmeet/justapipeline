pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'ap-south-1' // Replace with your AWS region
        AWS_CREDENTIALS = credentials('f2fdff07-436a-43cd-b9c8-6bce57a1c9cf') // Replace with your Jenkins credentials ID
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
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'f2fdff07-436a-43cd-b9c8-6bce57a1c9cf']]) {
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
