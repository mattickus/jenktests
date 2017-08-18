pipeline{
  agent any
  triggers {
        cron('H 4/* 0 0 1-5')
  }
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
      step([$class: 'GitHubPRCommentPublisher', comment: [content: 'Build ${BUILD_NUMBER} SUCCESS!']])
    }
    failure {
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "Failure", state: "FAILURE"]]]])
      step([$class: 'GitHubPRCommentPublisher', comment: [content: 'Build ${BUILD_NUMBER} FAILURE!']])
    }
    always {
      sh 'env | sort'
    }
  }
}
