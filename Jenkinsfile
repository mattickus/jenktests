pipeline {
  agent any
  stages {
    stage("build") {
      steps {
        echo "hello world!!!"
      }
    }
    stage("status") {
      steps {
        echo "hello world 2"
      }
    }
  }
  setBuildStatus("Build complete", "SUCCESS");
}
