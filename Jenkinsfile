pipeline{
  agent any
  triggers {
    cron('H 4 1 1 1-5')
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
        step([$class: 'GitHubPRCommentPublisher', comment: [content: 'Build ${BUILD_NUMBER} SUCCESS!']])
      }
    }
  }
  post {
    success {
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "Successful", state: "SUCCESS"]]]])
    }
    failure {
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "Failure", state: "FAILURE"]]]])
    }
    always {
      sh 'env | sort'
    }
  }
}
