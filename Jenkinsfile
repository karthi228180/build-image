pipeline {
    agent any

    environment{
	DOCKER_IMAGE = "myapp"
	DOCKER_TAG = "latest"
    }
    stages{
	stage ("code cloning"){
	    steps{
		echo "code cloning from github"
	    }			
	}
	stage ("Build docker image"){
	    steps {
		echo "Buid docker image"
		sh '''
		  docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
		'''
            }
	}
	stage ("verify Docker image"){
	    steps {
		sh '''
		  docker images
		'''
	    }
	}
	
    }

    post {
	success {
	   echo "Docker image built successfully"
	}
    }
}
