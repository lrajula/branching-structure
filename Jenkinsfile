pipeline {
  agent { node { label 'lb_sdl24798' } }
  stages {
    stage('build') {
      steps {
        sh 'echo Building ${BRANCH_NAME}...'
      }
    }
  }
}
