pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
    stage("set status") {
      steps {
        $class: 'GitHubCommitStatusSetter',
        reposSource: [$class: "ManuallyEnteredRepositorySource", url: repoUrl],
        commitShaSource: [$class: "ManuallyEnteredShaSource", sha: commitSha],
        errorHandlers: [[$class: 'ShallowAnyErrorHandler']],
        statusResultSource: [
          $class: 'ConditionalStatusResultSource',
            results: [
              [$class: 'BetterThanOrEqualBuildResult', result: 'SUCCESS', state: 'SUCCESS', message: build.description],
              [$class: 'BetterThanOrEqualBuildResult', result: 'FAILURE', state: 'FAILURE', message: build.description],
              [$class: 'AnyBuildResult', state: 'FAILURE', message: 'Loophole']
          ]
        ]
      }
    }
  }
}
