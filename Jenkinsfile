#!groovy
//
// QA Complex App tests Runner

// Pipeline
pipeline {
  agent {
    label 'master'
  }
  options {
    timeout(time: 1, unit: 'HOURS')
    timestamps()
  } // options
  stages {
    stage('\u2776 Test') {
      steps {
        script {
          currentBuild.displayName = "#${env.BUILD_NUMBER} (${env.GIT_COMMIT.take(8)}) ${env.GIT_BRANCH}"
          sh '''
            python3 -m pip install -r requirements.txt
            python3 -m pytest tests/ -n 4 --html=report.html --self-contained-html
          '''
        } // script
      } // steps
    } // stage
  } // stages
  post {
    always {
      archiveArtifacts artifacts: '**/*.png, **/*.html', allowEmptyArchive: true
      cleanWs()
    } // always
  } // post
} // pipeline

// vim: ft=groovy
// EOF
