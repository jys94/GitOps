node {
  stage('Clone repository') {
    slackSend(message: "Deploy ${env.BUILD_NUMBER} Started", color: 'good', tokenCredentialId: 'slack-key')
  }
  stage('Clone repository') {
    checkout scm
  }
  stage('git pull') {
    git url: 'https://github.com/jys94/GitOps.git', branch: 'Slack'
  }
  stage('Pull image') {
    sh 'docker pull 739362892804.dkr.ecr.ap-northeast-2.amazonaws.com/nginx:latest'
  }
  stage('Push image') {
    sh 'rm ~/.dockercfg || true'
    sh 'rm ~/.docker/config.json || true'

    docker.withRegistry('https://739362892804.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:jenkins-ecr-access-credential') {
      app.push("v1")
    }
  }
  stage('k8s deploy') {
    sh 'kubectl apply -f web-dpy.yaml'
  }
  stage('deploy end') {
    slackSend(message: """${env.JOB_NAME} #${env.BUILD_NUMBER} End
    """, color: 'good', tokenCredentialId: 'slack-key')
  }
}
