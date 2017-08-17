def setBuildStatus(String message, String state, String context, String sha) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/mattickus/jenktests"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: context],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      commitShaSource: [$class: "ManuallyEnteredShaSource", sha: sha ],
      statusBackrefSource: [$class: "ManuallyEnteredBackrefSource", backref: "${BUILD_URL}flowGraphTable/"],
      statusResultSource: [$class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

pipeline {
  agent any
  try {
    stages {
      stage("build") {
        steps {
          step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: []]])
          echo "hello world!!!"
          currentBuild.result = 'SUCCESS'
      }
    }
  } catch (Exception err) {
    currentBuild.result = 'FAILURE'
  }  
  stage("status") {
    steps {
      echo "${currentBuild.result}"
      step([$class: 'GitHubCommitStatusSetter', statusResultSource: [$class: 'ConditionalStatusResultSource', results: [[$class: "AnyBuildResult", message: "Successful", state: "${currentBuild.result}"]]]])
    }
  }
}


