pipeline {

   agent {
    node {
      label 'master'
    }
  }

   options {
    timestamps()
  }
  environment {  EMAIL_RECIPIENTS = "practicejenkins123@gmail.com"
 }

   stages {
    stage('PHPUnit Test') {
      steps {
        echo 'Running PHPUnit...'
	}
    }
    stage('Merge PR') {
      when {
        branch 'PR-*'
      }
      steps {
        sh 'git remote set-url origin git@github.com:practicejenkins123/sample-php-project.git'
        sh 'git remote set-branches --add origin ${CHANGE_TARGET}'
        sh 'git fetch origin'
        sh 'git checkout ${CHANGE_TARGET}'
        sh 'git merge --no-ff ${GIT_COMMIT}'
        sh 'git push origin ${CHANGE_TARGET}'
      }
    }
  }
	
 post{
	always{
		emailext to: "${env.EMAIL_RECIPIENTS}",
		body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
	}

	
}

}

