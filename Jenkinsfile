pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'echo Building ${BRANCH_NAME}...'
        
          script {
                          git_author=sh(returnStdout: true, script:'''
                              pull_json=`curl -u $USERNAME:$PASSWORD https://github.td.teradata.com/api/v3/repos/dbeties/tdm-mig/pulls/${CHANGE_ID} -sS`
                              commit_id=`echo ${pull_json} | python -c 'import json,sys;obj=json.load(sys.stdin);print obj["head"]["sha"]'`
                              author=`git --no-pager show -s --format='%an <%ae>' ${commit_id} | cut -d "<" -f2 | cut -d "@" -f1`
                              echo ${author}
                              ''').replace("\n","")
                        sh"""
                        echo '${git_author}'
                          """
                      }
        
        
        
        
      }
    }
  }
}
