pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world"
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
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: []]])
    }
  }
}
