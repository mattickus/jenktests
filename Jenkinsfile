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
      def theStatus = 'SUCCESS'
      def theComment = 'Successful'
    }
    failure {
      def theStatus = 'FAILURE'
      def theComment = 'Failed'
    }
    always {
      sh 'echo Done!'
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "${theComment}", state: "${theStatus}"]]]])
    }
  }
}
