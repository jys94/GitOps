app = docker.build("73936289280.dkr.ecr.ap-northeast-2.amazonaws.com/nginx")
docker.withRegistry('https://73936289280.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:jenkins-ecr-access-credential')

node {
    stage('Clone repository') {
        checkout scm
    }
    stage('git pull') {
      steps {
        git url: 'https://github.com/jys94/GitOps.git', branch: 'Test'
      }
    }
    stage('Build image') {
        app = docker.build("73936289280.dkr.ecr.ap-northeast-2.amazonaws.com/nginx")
    }
    stage('Push image') {
        sh 'rm ~/.dockercfg || true'
        sh 'rm ~/.docker/config.json || true'

        docker.withRegistry('https://73936289280.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:jenkins-ecr-access-credential') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
