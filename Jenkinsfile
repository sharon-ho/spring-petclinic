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
                bat './mvnw deploy -DaltDeploymentRepository=internal.repo::default::file:///C:/Users/Sharon/Documents/Concordia/Winter 2020/SOEN345/Assignments/Assignment 6/spring-petclinic'
            }
        }
  }
  post {
	success {
		emailext (
			subject: "Successful job: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			body: "The Jenkins job was successful: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
			recipientProviders: [[$class: 'DevelopersRecipientProvider']]
		)
	}
}
}