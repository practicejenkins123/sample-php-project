pipeline {

   agent {
    node {
      label 'master'
    }
  }

   options {
    timestamps()
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
}

