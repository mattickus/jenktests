pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
  }
  post {
    failure {
      echo "It was a failure"
      step([$class: 'GitHubPRBuildStatusPublisher', statusMsg: [content: '${GITHUB_PR_COND_REF} run ended'], statusVerifier: [buildStatus: 'SUCCESS'], unstableAs: 'FAILURE'])
    }
    success {
      echo "It was a success"
      step([$class: 'GitHubPRBuildStatusPublisher', statusMsg: [content: '${GITHUB_PR_COND_REF} run ended'], statusVerifier: [buildStatus: 'SUCCESS'], unstableAs: 'FAILURE'])
    }
  }
}
