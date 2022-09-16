pipeline{
  agent{
    docker{
	  image 'node:6-alpine'
	  args '-p 3007:3000 -p 5007:5000'
	}
  }
  environment{
    CI = 'true'
  }
  stages{
    stage('Build'){
	  steps{
	    sh 'npm install'
	  }
	}
	stage('Test'){
	  steps{
	    sh './jenkins/scripts/test.sh'
	  }
	}
	stage('Diliver for production') {
	  when {
	    branch 'production'
	  }
	  steps {
	    sh './jenkins/scripts/deliver-for-production.sh'
		input messages 'Finished using the web site? (Click "Proceed" to continue)'
		sh './jenkins/scripts/kill.sh'
	  }
	}
	stage('Diliver for development') {
	  when {
	    branch 'development'
	  }
	  steps {
	    sh './jenkins/scripts/deploy-for-development.sh'
		input message: 'Finished using the web site? (Click "Proceed" to continue)'
		sh './jenkins/scripts/kill.sh'
	  }
	}
  }
}
