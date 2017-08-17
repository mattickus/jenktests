def setBuildStatus(String message, String state, String context, String sha) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/<yourRepoURL>"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: context],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      commitShaSource: [$class: "ManuallyEnteredShaSource", sha: sha ],
      statusBackrefSource: [$class: "ManuallyEnteredBackrefSource", backref: "${BUILD_URL}flowGraphTable/"],
      statusResultSource: [$class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        setBuildStatus("In Progress","PENDING",jobContext,"${gitCommit}")
        echo "hello world!!!"
      }
    }
    stage("status") {
      steps {
        echo "hello world 2"
        setBuildStatus("Complete","FAILURE",jobContext,"${gitCommit}")
        setBuildStatus("Complete","SUCCESS",jobContext,"${gitCommit}")
      }
    }
  }
}


