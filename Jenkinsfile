pipeline {
  agent any
  stages {
    stage('deploy start') {
      steps {
        slackSend(message: "Deploy ${env.BUILD_NUMBER} Started"
        , color: 'good', tokenCredentialId: 'slack-key')
      }
    }      
    stage('git pull') {
      steps {
        git url: 'https://github.com/jys94/GitOps.git', branch: 'Slack'
      }
    }
    stage('k8s deploy'){
      steps {
        sh '''
        docker pull nginx
        docker tag nginx:latest 739362892804.dkr.ecr.ap-northeast-2.amazonaws.com/nginx:latest
        docker push 739362892804.dkr.ecr.ap-northeast-2.amazonaws.com/nginx:latest
        kubectl apply -f ./
        '''
      }
    }
    stage('deploy end') {
      steps {
        slackSend(message: """${env.JOB_NAME} #${env.BUILD_NUMBER} End
        """, color: 'good', tokenCredentialId: 'slack-key')
      }
    }
  }
}
