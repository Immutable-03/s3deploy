pipeline {
  agent any

  stages {
    stage('Install Dependencies') {
      steps {
        script {
          echo "sss"
          sh 'npm install'
        }
      }
    }

    stage('Build') {
      steps {
        script {
          sh 'npm run build'
          echo 'success'
        }
      }
    }

    stage('deploy') {
            steps {
              // bat "aws configure set region $AWS_DEFAULT_REGION" 
              sh "aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID"  
              sh "aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY"
              // bat "aws s3 cp ivica/index.html s3://ivica"
              sh 'aws s3 sync build/ s3://appreactjs'
              echo 'success'
            }
        }
  }
}