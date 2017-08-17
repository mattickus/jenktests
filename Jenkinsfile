pipeline{
  agent any
  stages {
    stage("Test Puppet") {
      steps {
        sh '/usr/local/bin/puppet parser validate .'
        sh '/usr/bin/yamllint .'
      }
    }
    stage("Test YAML") {
      steps {
        
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
  }
}
