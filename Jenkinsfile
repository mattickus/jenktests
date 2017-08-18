pipeline{
  agent any
  stages {
    stage("Test Puppet") {
      steps {
        sh '/usr/local/bin/puppet parser validate .'
      }
    }
    stage("Test YAML") {
      steps {
        sh '/usr/bin/yamllint .'        
      }
    }
  }
  post {
    success {
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "Successful", state: "SUCCESS"]]]])
      step([$class: 'GitHubPRCommentPublisher', comment: [content: 'Build ${BUILD_NUMBER} ${BUILD_STATUS}']])
    }
    failure {
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "Failure", state: "FAILURE"]]]])
      step([$class: 'GitHubPRCommentPublisher', comment: [content: 'Build ${BUILD_NUMBER} ${BUILD_STATUS}']])
    }
    always {
      sh 'echo Done'
    }
  }
}
