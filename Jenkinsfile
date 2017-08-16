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
      step([$class: 'GitHubPRBuildStatusPublisher', statusMsg: [content: 'failed'], unstableAs: 'FAILURE'])
    }
    success {
      echo "It was a success"
      step([$class: 'GitHubPRBuildStatusPublisher', statusMsg: [content: 'success'], unstableAs: 'FAILURE'])
    }
  }
}
