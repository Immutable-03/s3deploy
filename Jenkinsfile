pipeline {
  agent any

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

    stage('Deploy') {
      steps {
        withCredentials([string(credentialsId: 'AKIATOWQFZCJX67ZUSJY', variable: 'AWS_ACCESS_KEY_ID'),
                        string(credentialsId: 'AKIATOWQFZCJX67ZUSJY', variable: 'AWS_SECRET_ACCESS_KEY')]) {
          script {
            sh 'aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID'
            sh 'aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY'
            sh 'aws s3 sync build/ s3://appreactjs'
          }
        }
      }
    }
  }
}
