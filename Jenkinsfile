void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/prasadambasaveswar/testshell.git"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/prasadambasaveswar/testshell.git'
            }
        }
        stage('build') {
        steps {
        sh 'sh -x $WORKSPACE/test.sh'
        }
        }
    }
    
  post {
    success {
        setBuildStatus("Build succeeded", "SUCCESS");
    }
    failure {
        setBuildStatus("Build failed", "FAILURE");
    }
  }
  }
