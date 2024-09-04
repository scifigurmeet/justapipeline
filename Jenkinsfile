pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Deploy to AWS') {
            steps {
                withAWS(credentials: '8c97472c-381f-4e1a-9ee6-3e8526d15888', region: 'us-west-2') {
                    sh 'aws deploy create-deployment --application-name web-app --deployment-group-name web-deployment-group --github-location repository=scifigurmeet/justapipeline,commitId=${GIT_COMMIT}'
                }
            }
        }
    }
}
