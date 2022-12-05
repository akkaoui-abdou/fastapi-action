pipeline {
	
	
  	//agent { label 'linux' }
	agent any
	
	options {
		buildDiscarder(logRotator(numToKeepStr:'5'))
	}
  
	environment {
		DOCKERHUB_CREDENTIALS = credentials('credential-docker')
	}
  
  stages {
	  
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/akkaoui-abdou/fastapi-action.git', branch: 'main', credentialsId: 'github-credentials')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }
	  
	  
     stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
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
