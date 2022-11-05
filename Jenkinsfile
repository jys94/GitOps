pipeline {
  agent any
  stages {
    stage('git pull') {
      steps {
        git url: 'https://github.com/jys94/GitOps.git', branch: 'Test'
      }
    stage('docker build'){
      steps {
        sh '''
        docker build -t nginx .
        '''
      }
    }
    }
  }
}

node {
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        app = docker.build("739362892804.dkr.ecr.ap-northeast-2.amazonaws.com/nginx")
    }
    stage('Push image') {
        sh 'rm ~/.dockercfg || true'
        sh 'rm ~/.docker/config.json || true'

        docker.withRegistry('https://739362892804.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:jenkins-ecr-access-credential') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
