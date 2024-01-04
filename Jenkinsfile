pipeline {
  agent any
  environment{
    AWS_ACCESS_KEY_ID = credentials(AKIATOWQFZCJX67ZUSJY).AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY = credentials(AKIATOWQFZCJX67ZUSJY).AWS_SECRET_ACCESS_KEY
  }

  stages {
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
          echo 'success'
        }
      }
    }

    stage('deploy') {
            steps {
              sh "aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID"  
              sh "aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY"
              sh 'aws s3 sync build/ s3://appreactjs'
            }
        }
  }
}
