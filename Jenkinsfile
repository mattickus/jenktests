pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
    stage("status") {
      steps {
        step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [message: 'Success!', result: 'SUCCESS', state: 'SUCCESS']]])
      }
    }
  }
}
