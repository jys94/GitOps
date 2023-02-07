node {
  stage('Clone repository') {
    checkout scm
  }
  stage('git pull') {
    git url: 'https://github.com/jys94/GitOps.git', branch: 'Test'
  }
  stage('Build image') {
    app = docker.build("117612009356.dkr.ecr.ap-northeast-2.amazonaws.com/nginx")
  }
  stage('Push image') {
    sh 'rm ~/.dockercfg || true'
    sh 'rm ~/.docker/config.json || true'

    docker.withRegistry('https://117612009356.dkr.ecr.ap-northeast-2.amazonaws.com/nginx', 'ecr:ap-northeast-2:jenkins-ecr-access-credential') {
      app.push("latest")
    }
  }
  stage('k8s deploy') {
    sh 'kubectl apply -f nginx-test.yaml'
  }
}
