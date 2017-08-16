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
      step([$class: 'GitHubSetCommitStatusBuilder'])
    }
    success {
      echo "It was a success"
      step([$class: 'GitHubSetCommitStatusBuilder'])
    }
  }
}
