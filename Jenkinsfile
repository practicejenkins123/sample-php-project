pipeline {

  agent any

  options {
    timestamps()
  }

  stages {
    stage('PHPUnit Test') {
      steps {
        echo 'Running PHPUnit...'
        sh '/bin/phpunit ${WORKSPACE}/src'
      }
    }
  }

  post {
    failure {
      slackSend "Build failed - Job: failed"
    }
    changed {
      slackSend "Build status changed - Job: Changed"
    }
  }
}
