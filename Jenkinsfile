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
	
	stage ("docker login"){
	    steps {
		echo "login in to dockehub using credntials"
		withCredentials([usernamePassword(credentialsId: "Dockerhub",usernameVariable:"dockerHubUser", 
		passwordVariable:"dockerHubPass") )]
		{
		  sh '''
		    docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}
		  '''
		}
	    }
	}
	
	stage ("push to dockerhub"){
	    steps {
		sh '''
		  docker push  ${env.dockerHubUser}/$DOCKER_IMAGE:$DOCKER_TAG
		'''	
    }

    post {
	success {
	   echo "Docker image built successfully"
	}
    }
}

