def git_author
def mail_extension="@gmail.com"
pipeline {
  agent { node { label 'AnsibleSlave' } }
  stages {
    stage('build') {
      steps {
        sh 'echo Building ${BRANCH_NAME}...'
        
          script {
                        def selectedBranch = [[name: "${BRANCH_NAME}"]]
                        checkout([$class: 'GitSCM', branches: selectedBranch,
                                doGenerateSubmoduleConfigurations: false,
                                extensions: [],
                                submoduleCfg: [],
                                userRemoteConfigs: [[credentialsId: 'personal-github-access-lrajula', url: 'https://github.com/lrajula/branching-structure.git']]])
                          git_author = sh(returnStdout: true, script: '''
                        current_commit=`git branch  | grep "*" | cut -d " " -f5 | cut -d ")" -f1`
                        author=`git --no-pager show -s --format='%an <%ae>' ${current_commit} | cut -d "<" -f2 | cut -d "@" -f1`
                        echo ${author}''').split()[0].replace("]", "").replace("[", "")
                        sh """echo ${git_author}"""
                      }

        
      }
    }
  }
  
  post {
        success {
            emailext (
        subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
        body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
          <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
        recipientProviders: [[$class: 'DevelopersRecipientProvider']]
      )
        }
  }
  
  
}
