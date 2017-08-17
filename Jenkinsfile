pipeline{
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
    stage("status") {
      steps {
        echo "${currentBuild.result}"
        sh 'ls -l'
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
