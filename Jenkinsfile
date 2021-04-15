library("tdr-jenkinslib")

pipeline {
  agent {
    label "master"
  }

  stages {
    stage("Run git secrets") {
      steps {
        script {
          def exitCode = sh(script: "git-secrets --scan", returnStatus: true)
          def scanOutput = sh(script: "git-secrets --scan 2>&1 >/dev/null | head -n 4 | cut -c1-6 | tr -d '\n'", returnStdout: true)
          if (exitCode == 0 || scanOutput.trim() != "test:1test:3test:5") {
            tdr.postToDaTdrSlackChannel(colour: "danger", message: "*Security test failure*: expected Jenkins to detect sensitive information but it did not. Check that git-secrets is installed and configured on Jenkins.\n${env.BUILD_URL}")
          }
        }
      }
    }
  }
  post {
    failure {
      node('master') {
        script {
          tdr.postToDaTdrSlackChannel(colour: "danger", message: "*The git secrets check on Jenkins has failed.* \n${env.BUILD_URL}")
        }
      }
    }
  }
}
