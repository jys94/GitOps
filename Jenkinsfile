pipeline {
  agent any
  stages {
    stage('git pull') {
      steps {
        // https://github.com/jys94/GitOps.git will replace by sed command before RUN
        git url: 'https://github.com/jys94/GitOps.git', branch: 'main'
      }
    }
    stage('k8s deploy'){
      steps {
        sh '''
        kubectl apply -f .
        '''
      }
    }    
  }
}
