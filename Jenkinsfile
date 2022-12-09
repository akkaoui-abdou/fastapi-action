pipeline {
	
	
  	//agent { label 'docker-build-node' }
	//agent any
	
	agent {
        	docker { image 'ubuntu:latest' }
   	}
	
	options {
		buildDiscarder(logRotator(numToKeepStr:'5'))
	}
  
	environment {
		DOCKERHUB_CREDENTIALS = credentials('credentials-docker')
	}
  
  stages {
	  
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/akkaoui-abdou/fastapi-action.git', branch: 'main', credentialsId: 'credentials-github')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
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
