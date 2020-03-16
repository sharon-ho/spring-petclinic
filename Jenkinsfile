pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        slackSend (color: '#00FF00', message: "Building: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        bat './mvnw clean install'
      }
    }
    
    stage('Test') {
        steps {
            slackSend (color: '#00FF00', message: "Testing: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            bat './mvnw test' 
        }
    }
      
    stage('Package') {
        steps {
            slackSend (color: '#00FF00', message: "Packaging: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            bat './mvnw package' 
        }
    }

    stage('Deploy') {
    when {
        branch 'master'
    }
        steps {
            slackSend (color: '#00FF00', message: "Deploying: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            bat './mvnw deploy -DaltDeploymentRepository=internal.repo::default::file:///C:/Users/Sharon/Desktop/Deploy'
        }
    }
  }
  post {
	success {
		slackSend (color: '#00FF00', message: "Build Success! '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
	}
}
}