pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
    stage("set status") {
      steps {
        step([$class: 'GitHubCommitStatusSetter'])
      }
    }
  }
}
