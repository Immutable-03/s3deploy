pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AKIATOWQFZCJX67ZUSJY')
        AWS_SECRET_ACCESS_KEY = credentials('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')
        AWS_DEFAULT_REGION    = 'ap-south-1'
        S3_BUCKET             = 'appreactjs'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy to S3') {
            steps {
                script {
                    sh """
                        aws configure set aws_access_key_id ${AWS_ACCESS_KEY_ID}
                        aws configure set aws_secret_access_key ${AWS_SECRET_ACCESS_KEY}
                        aws configure set region ${AWS_DEFAULT_REGION}
                        aws s3 sync dist/ s3://${S3_BUCKET}/
                    """
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
