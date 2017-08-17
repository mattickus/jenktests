pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
  }
  step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: 'BetterThanOrEqualBuildResult', message: 'Success!', result: 'SUCCESS', state: 'SUCCESS']]]])
}
