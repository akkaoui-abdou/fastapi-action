pipeline {
	
	 def app
  	//agent { label 'docker-build-node' }
	agent any

	/*
	options {
		buildDiscarder(logRotator(numToKeepStr:'5'))
	}
  	*/
	
	environment {
		DOCKERHUB_CREDENTIALS = credentials('credentials-docker')
	}
  
  stages {
	  
	  
    /*
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/akkaoui-abdou/fastapi-action.git', branch: 'main', credentialsId: 'credentials-github')
      }
    }
    */

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }
	  
    stage('Build') {
      steps {
       // sh 'docker build -t akkaoui/fastapi-gitaction:latest .'
	 app = docker.build("akkaoui/fastapi-gitaction")
      }
     }
	
/*	  
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
	  
*/
	  
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'credentials-docker') {
            app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
        }
    }
	  

  }
  
	/*
  	post {
		always {
		    sh 'docker logout'
		}
	}
	*/
	
}
