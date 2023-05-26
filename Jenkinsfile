pipeline {
    agent any
    
    environment {
        //DOCKERHUB_USERNAME = 'Venky02'
        DOCKERHUB_CREDENTIALS = credentials('Venky')
        DOCKER_IMAGE_NAME = 'hotstar'
        DOCKERHUB_REPO = 'venky02/myngnix'
        DOCKERFILE_PATH = '/var/lib/jenkins/workspace/Dockerdeploy/Dockerfile'
	DOCKER_CONTAINER = 'my-first-nginx'
    }
    
    stages {
        stage('Welcome') { 
            steps { 
               echo 'This Build will create a Docker Container' 
            }
        }
        stage('Pull Sources') {
            steps {
		    git url: 'https://github.com/Venky055/docker-cicd.git', branch: 'main'
		    //sh 'chmod +x /var/lib/jenkins/workspace/DockerImage/'
            }
         }
	 
	 stage('Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE_NAME .'
            }
        }
	
	stage('Push to Docker Hub') {
            steps {
		    sh 'docker run -d --name $DOCKER_CONTAINER -p 8070:80 $DOCKER_IMAGE_NAME'
		    sh 'docker ps'
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR -p Lovelly@2'
                    sh 'docker tag $DOCKER_IMAGE_NAME $DOCKERHUB_REPO'
            }
        }
        
	    
	      stage ('Deploy') {
          steps {
		  sh 'docker push $DOCKERHUB_REPO'
            	  echo 'Docker Image has been Successfully Pushed to Docker Hub'
                }
	    }  	       
    }
}
