pipeline {
	
	
  	agent { label 'linux' }
	
	options {
		buildDiscarder(logRotator(numToKeepStr:'5'))
	}
  
	environment {
		DOCKERHUB_CREDENTIALS = credentials('credential-docker')
	}
  

    stage('Build') {
      steps {
        sh 'docker build -t akkaoui/fastapi-gitaction:latest .'
      }
    }
	
	
	stage('Login into Dockerhub') {
		steps {
		 sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		}
	}


    stage('Push') {
      steps {
        sh 'docker push akkaoui/fastapi-gitaction:latest'
      }
    }

  }
  
  	post {
		always {
		    sh 'docker logout'
		}
	}
	
	
}
