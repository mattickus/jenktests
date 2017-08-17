pipeline{
  agent any
  environment {
    def theStatus = 'SUCCESS'
    def theComment = 'Successful'
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
      theStatus = 'SUCCESS'
      theComment = 'Successful'
    }
    failure {
      theStatus = 'FAILURE'
      theComment = 'Failed'
    }
    always {
      sh 'echo Done!'
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "${theComment}", state: "${theStatus}"]]]])
    }
  }
}
