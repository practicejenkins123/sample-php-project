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
      slackSend message: "Build failed - Job: ${JOB_NAME} - Build No.: ${BUILD_NUMBER} - Build URL: (<${BUILD_URL}|Open>)"
    }
    changed {
      slackSend message: "Build status changed - Job: ${JOB_NAME} - Build No.: ${BUILD_NUMBER} - Build URL: (<${BUILD_URL}|Open>)"
    }
  }
}
