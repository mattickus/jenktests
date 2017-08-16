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
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: []]])
    }
    success {
      echo "It was a success"
      step([$class: 'GitHubPRBuildStatusPublisher', buildMessage: [failureMsg: [content: 'Can\'t set status; build failed.'], successMsg: [content: 'Can\'t set status; build succeeded.']], statusMsg: [content: '${GITHUB_PR_COND_REF} run ended'], unstableAs: 'FAILURE'])
    }
  }
}
