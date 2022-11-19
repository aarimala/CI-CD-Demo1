pipeline {
  agent any
  
  tools
  {
	maven 'Maven'
  }
  stages {
    stage ('SCM Checkout') {
      steps {
                //git branch: 'main', url: 'https://github.com/aarimala/CI-CD-demo.git'
	     git branch: 'main', url: 'https://github.com/aarimala/CI-CD-Demo1.git'
      }
      }
 stage ('Excute Maven') {
      steps {
        sh 'mvn package'
      }
    }
	  stage ('docker build and tag') {
      steps {
        sh 'docker build -t my-webapp:latest .'
        sh 'docker tag my-webapp arifarimala/my-webapp:1.0'
      }
    }
    stage ('publish image to dockerhub') {
	 steps {	   
        withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub1')]) {
	sh 'docker login -u arifarimala -p ${MyDocker-Arif-ID}'   
}
		sh 'docker push arifarimala/my-webapp:1.0'
		}
		}
	 stage ('Run Docker container on Jenkins Agent') {
		 steps {  
			 sh "docker run -d -p 8003:8080 arifarimala/my-webapp"
               	
                
		sh "docker -H ssh://ec2-user@15.207.109.77/ run arifarimala/my-webapp"
			
         }  
	 }
  }
}
